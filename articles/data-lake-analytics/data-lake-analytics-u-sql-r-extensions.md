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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="294cd-103">Öğretici: U-SQL R ile genişletme ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="294cd-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="294cd-104">Aşağıdaki örneğine hello hello R kodu dağıtmak için temel adımlar gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="294cd-104">hello following example illustrates hello basic steps for deploying R code:</span></span>
* <span data-ttu-id="294cd-105">Kullanım hello `REFERENCE ASSEMBLY` hello U-SQL betiği için deyimi tooenable R uzantıları.</span><span class="sxs-lookup"><span data-stu-id="294cd-105">Use hello `REFERENCE ASSEMBLY` statement tooenable R extensions for hello U-SQL Script.</span></span>
* <span data-ttu-id="294cd-106">Kullanım` REDUCE` işlemi toopartition hello giriş verileri bir anahtarı.</span><span class="sxs-lookup"><span data-stu-id="294cd-106">Use the` REDUCE` operation toopartition hello input data on a key.</span></span>
* <span data-ttu-id="294cd-107">U-SQL için Hello R uzantıları dahil yerleşik reducer (`Extension.R.Reducer`) her atanan köşe toohello reducer R kodu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="294cd-107">hello R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned toohello reducer.</span></span> 
* <span data-ttu-id="294cd-108">Ayrılmış kullanımını adlı adlı veri çerçevelerini `inputFromUSQL` ve `outputToUSQL `sırasıyla toopass veri U-SQL, r giriş ve çıkış arasında DataFrame tanımlayıcı adları düzeltilen (diğer bir deyişle, kullanıcıların bu önceden tanımlanmış adları giriş değiştirip edemezsiniz DataFrame çıkış tanımlayıcılar).</span><span class="sxs-lookup"><span data-stu-id="294cd-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively toopass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-hello-u-sql-script"></a><span data-ttu-id="294cd-109">R kodu hello U-SQL betiği katıştırma</span><span class="sxs-lookup"><span data-stu-id="294cd-109">Embedding R code in hello U-SQL script</span></span>

<span data-ttu-id="294cd-110">Hello hello komut parametresini kullanarak, U-SQL betiği yapabilecekleriniz satır içi hello R kodu `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="294cd-110">You can inline hello R code your U-SQL script by using hello command parameter of hello `Extension.R.Reducer`.</span></span> <span data-ttu-id="294cd-111">Örneğin, hello R betiği olarak bir dize değişkeni bildirme ve parametre toohello Reducer geçirin.</span><span class="sxs-lookup"><span data-stu-id="294cd-111">For example, you can declare hello R script as a string variable and pass it as a parameter toohello Reducer.</span></span>


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

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a><span data-ttu-id="294cd-112">Ayrı bir dosyaya Hello R kodu tutmak ve hello U-SQL betiği başvuru</span><span class="sxs-lookup"><span data-stu-id="294cd-112">Keep hello R code in a separate file and reference it  hello U-SQL script</span></span>

<span data-ttu-id="294cd-113">Aşağıdaki örneğine hello daha karmaşık bir kullanımı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="294cd-113">hello following example illustrates a more complex usage.</span></span> <span data-ttu-id="294cd-114">Bu durumda, hello R kodu hello U-SQL betiği olan bir kaynak olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="294cd-114">In this case, hello R code is deployed as a RESOURCE that is hello U-SQL script.</span></span>

<span data-ttu-id="294cd-115">Bu R kodu ayrı bir dosya olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="294cd-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="294cd-116">U-SQL komut dosyası toodeploy dağıtmak kaynağı deyim hello ile bu R betiği kullanın.</span><span class="sxs-lookup"><span data-stu-id="294cd-116">Use a U-SQL script toodeploy that R script with hello DEPLOY RESOURCE statement.</span></span>

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

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="294cd-117">R U-SQL ile nasıl tümleşik çalıştığını</span><span class="sxs-lookup"><span data-stu-id="294cd-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="294cd-118">Veri türleri</span><span class="sxs-lookup"><span data-stu-id="294cd-118">Datatypes</span></span>
* <span data-ttu-id="294cd-119">U-SQL dizesi ve sayısal sütunlarından olarak dönüştürülür-R DataFrame ve U-SQL arasında [desteklenen türleri: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="294cd-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="294cd-120">Merhaba `Factor` U-SQL veri türü desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="294cd-120">hello `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="294cd-121">`byte[]`bir base64 ile kodlanmış serileştirilmesi gereken `string`.</span><span class="sxs-lookup"><span data-stu-id="294cd-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="294cd-122">U-SQL dizeleri, R kodda, dönüştürülmüş toofactors olabilir, U-SQL oluşturduktan sonra R giriş dataframe veya ayarı hello reducer parametresi tarafından `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="294cd-122">U-SQL strings can be converted toofactors in R code, once U-SQL create R input dataframe or by setting hello reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="294cd-123">Şemalar</span><span class="sxs-lookup"><span data-stu-id="294cd-123">Schemas</span></span>
* <span data-ttu-id="294cd-124">U-SQL veri kümeleri yinelenen sütun adlarına sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="294cd-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="294cd-125">U-SQL veri kümeleri sütun adlarının dize olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="294cd-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="294cd-126">Sütun adları gerekir olması hello U-SQL ve R komut dosyalarında aynı.</span><span class="sxs-lookup"><span data-stu-id="294cd-126">Column names must be hello same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="294cd-127">ReadOnly sütunu hello çıktı dataframe parçası olamaz.</span><span class="sxs-lookup"><span data-stu-id="294cd-127">Readonly column cannot be part of hello output dataframe.</span></span> <span data-ttu-id="294cd-128">UDO çıktı şeması parçasıysa, salt okunur sütunlar otomatik olarak geri hello U-SQL tabloda eklenmiş çünkü.</span><span class="sxs-lookup"><span data-stu-id="294cd-128">Because readonly columns are automatically injected back in hello U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="294cd-129">İşlev sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="294cd-129">Functional limitations</span></span>
* <span data-ttu-id="294cd-130">Merhaba R altyapısı içinde iki kez başlatılamaz hello aynı işlemi.</span><span class="sxs-lookup"><span data-stu-id="294cd-130">hello R Engine can't be instantiated twice in hello same process.</span></span> 
* <span data-ttu-id="294cd-131">Şu anda, U-SQL için tahmini Reducer Udo'lar kullanılarak oluşturulan bölümlenmiş modelleri kullanarak Birleştirici Udo'lar desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="294cd-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="294cd-132">Kullanıcılar kaynak olarak bölümlenmiş hello modelleri bildirme ve bunların R betiği kullanın (örnek kodu görmek `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="294cd-132">Users can declare hello partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="294cd-133">R sürümleri</span><span class="sxs-lookup"><span data-stu-id="294cd-133">R Versions</span></span>
<span data-ttu-id="294cd-134">Yalnızca R 3.2.2 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="294cd-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="294cd-135">Standart R modülleri</span><span class="sxs-lookup"><span data-stu-id="294cd-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="294cd-136">Giriş ve çıkış boyutu sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="294cd-136">Input and Output size limitations</span></span>
<span data-ttu-id="294cd-137">Her köşe sınırlı bir tooit atanan bellek miktarı var.</span><span class="sxs-lookup"><span data-stu-id="294cd-137">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="294cd-138">Merhaba giriş ve çıkış DataFrames hello R kodu bellekte varolması gerektiğinden, hello toplam boyutu hello giriş ve çıkış için 500 MB aşamaz.</span><span class="sxs-lookup"><span data-stu-id="294cd-138">Because hello input and output DataFrames must exist in memory in hello R code, hello total size for hello input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="294cd-139">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="294cd-139">Sample Code</span></span>
<span data-ttu-id="294cd-140">Merhaba U-SQL Advanced Analytics extensions yüklendikten sonra daha fazla örnek kod, Data Lake Store hesabınızdaki kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="294cd-140">More sample code is available in your Data Lake Store account after you install hello U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="294cd-141">Daha fazla örnek kod Hello yoludur: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="294cd-141">hello path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="294cd-142">U-SQL ile özel R modülleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="294cd-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="294cd-143">İlk olarak, bir R özel modülü oluşturun ve onu zip ve R özel modülü dosya tooyour ADL deposu daraltılmış hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="294cd-143">First, create an R custom module and zip it and then upload hello zipped R custom module file tooyour ADL store.</span></span> <span data-ttu-id="294cd-144">Merhaba örnekte, biz magittr_1.5.zip toohello hello varsayılan ADLS hesabına hello kullanıyoruz ADLA hesap için kökündeki yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="294cd-144">In hello example, we will upload magittr_1.5.zip toohello root of hello default ADLS account for hello ADLA account we are using.</span></span> <span data-ttu-id="294cd-145">Merhaba modülü tooADL deposu karşıya yükledikten sonra dağıtmak kaynak toomake kullandıkça bildirirken, U-SQL komut dosyasını ve arama bulunan `install.packages` tooinstall.</span><span class="sxs-lookup"><span data-stu-id="294cd-145">Once you upload hello module tooADL store, declare it as use DEPLOY RESOURCE toomake it available in your U-SQL script and call `install.packages` tooinstall it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="294cd-146">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="294cd-146">Next Steps</span></span>
* [<span data-ttu-id="294cd-147">Microsoft Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="294cd-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="294cd-148">Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="294cd-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="294cd-149">Azure Data Lake Analytics işleri için U-SQL penceresi işlevlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="294cd-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
