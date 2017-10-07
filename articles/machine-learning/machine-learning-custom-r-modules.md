---
title: "Azure Machine learning'de özel R modülleri aaaAuthor | Microsoft Docs"
description: "Azure Machine learning'de özel R modülleri yazma için hızlı başlangıç."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="d0e18-103">Azure Machine Learning'de özel R modülleri yazma</span><span class="sxs-lookup"><span data-stu-id="d0e18-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="d0e18-104">Bu konuda açıklanmaktadır nasıl tooauthor ve Azure Machine learning'de özel R modülü dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d0e18-104">This topic describes how tooauthor and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="d0e18-105">Özel R modülleri nelerdir ve hangi dosyaları kullanılan toodefine açıklar bunları.</span><span class="sxs-lookup"><span data-stu-id="d0e18-105">It explains what custom R modules are and what files are used toodefine them.</span></span> <span data-ttu-id="d0e18-106">Nasıl tooconstruct hello bir modülün tanımlanması dosyaları ve nasıl tooregister hello Machine Learning çalışma alanındaki dağıtım için modülü gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-106">It illustrates how tooconstruct hello files that define a module and how tooregister hello module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="d0e18-107">Merhaba öğeleri ve özniteliklerinin hello özel modülü hello tanımında kullanılan sonra daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-107">hello elements and attributes used in hello definition of hello custom module are then described in more detail.</span></span> <span data-ttu-id="d0e18-108">Nasıl toouse yardımcı işlevleri, dosya ve birden çok çıkış da ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-108">How toouse auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="d0e18-109">Özel bir R Modülü nedir?</span><span class="sxs-lookup"><span data-stu-id="d0e18-109">What is a custom R module?</span></span>
<span data-ttu-id="d0e18-110">A **özel Modülü** olan olabilir kullanıcı tanımlı bir modül karşıya tooyour çalışma ve bir Azure Machine Learning deneme bir parçası olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="d0e18-110">A **custom module** is a user-defined module that can be uploaded tooyour workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="d0e18-111">A **özel R Modülü** kullanıcı tanımlı bir R işlev yürüten özel bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="d0e18-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="d0e18-112">**R** istatistiksel bilgi işlem ve istatistikçiler ve veri bilimcilerine tarafından algoritmaları uygulamak için yaygın olarak kullanılan grafik için bir programlama dilidir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="d0e18-113">Şu anda R özel modüller, ancak destek ek dilleri zamanlandığı yönelik için gelecek sürümlerde desteklenen hello yalnızca bir dildir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-113">Currently, R is hello only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="d0e18-114">Özel modüller sahip **birinci sınıf durum** Azure Machine learning'de hello herkese açık bunlar diğer modülü gibi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-114">Custom modules have **first-class status** in Azure Machine Learning in hello sense that they can be used just like any other module.</span></span> <span data-ttu-id="d0e18-115">Yayımlanan denemeler veya görselleştirmeleri dahil, diğer modüllerle çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="d0e18-116">Hello modülü tarafından uygulanan hello algoritması üzerinde denetim sahibi, kullanılan giriş ve çıkış bağlantı noktaları toobe Merhaba, modelleme parametreleri ve diğer çeşitli çalışma zamanı davranışları hello.</span><span class="sxs-lookup"><span data-stu-id="d0e18-116">You have control over hello algorithm implemented by hello module, hello input and output ports toobe used, hello modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="d0e18-117">Özel modüller içeren bir deney, Cortana Intelligence Galerisi hello kolay paylaşımı için de yayımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-117">An experiment that contains custom modules can also be published into hello Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="d0e18-118">Özel bir R Modülü dosyaları</span><span class="sxs-lookup"><span data-stu-id="d0e18-118">Files in a custom R module</span></span>
<span data-ttu-id="d0e18-119">Özel bir R modülü, en az iki dosyalarını içeren bir .zip dosyası tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d0e18-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="d0e18-120">A **kaynak dosyası** hello modülü tarafından kullanıma sunulan hello R işlevi uygular</span><span class="sxs-lookup"><span data-stu-id="d0e18-120">A **source file** that implements hello R function exposed by hello module</span></span>
* <span data-ttu-id="d0e18-121">Bir **XML tanım dosyasını** hello özel modülü arabirimi açıklanmaktadır</span><span class="sxs-lookup"><span data-stu-id="d0e18-121">An **XML definition file** that describes hello custom module interface</span></span>

<span data-ttu-id="d0e18-122">Ek yardımcı dosyalar da hello özel modülünden erişilebilir işlevselliği sağlayan hello .zip dosya eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-122">Additional auxiliary files can also be included in hello .zip file that provides functionality that can be accessed from hello custom module.</span></span> <span data-ttu-id="d0e18-123">Bu seçenek hello ele alınmıştır **bağımsız değişkenleri** hello başvuru bölümünde parçası **hello XML tanım dosyasını öğelerinde** hello hızlı başlangıç örnek aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="d0e18-123">This option is discussed in hello **Arguments** part of hello reference section **Elements in hello XML definition file** following hello quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="d0e18-124">Hızlı Başlangıç örnek: tanımlamak, paket ve özel bir R modülü kaydetme</span><span class="sxs-lookup"><span data-stu-id="d0e18-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="d0e18-125">Bu örnek nasıl tooconstruct hello özel bir R modülü tarafından gerekli olan dosyaları gösterir, bunları bir zip dosyası ve ardından kayıt hello modülü Machine Learning çalışma alanınızdaki paketi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-125">This example illustrates how tooconstruct hello files required by a custom R module, package them into a zip file, and then register hello module in your Machine Learning workspace.</span></span> <span data-ttu-id="d0e18-126">Merhaba örnek zip paketini ve örnek dosyaları yüklenebilir [CustomAddRows.zip karşıdan dosya](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d0e18-126">hello example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="hello-source-file"></a><span data-ttu-id="d0e18-127">Merhaba kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="d0e18-127">hello source file</span></span>
<span data-ttu-id="d0e18-128">Hello örneği göz önünde bulundurun bir **özel Add Rows** hello hello standart uygulaması değiştirir Modülü **Add Rows** modülü kullanılan iki veri kümesi (veri çerçevelerini) tooconcatenate satırları (gözlemleri).</span><span class="sxs-lookup"><span data-stu-id="d0e18-128">Consider hello example of a **Custom Add Rows** module that modifies hello standard implementation of hello **Add Rows** module used tooconcatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="d0e18-129">Merhaba standart **Add Rows** modülü hello ikinci girdi veri kümesi toohello sonuna hello kullanarak hello ilk girdi veri kümesi hello satırlarını ekler `rbind` algoritması.</span><span class="sxs-lookup"><span data-stu-id="d0e18-129">hello standard **Add Rows** module appends hello rows of hello second input dataset toohello end of hello first input dataset using hello `rbind` algorithm.</span></span> <span data-ttu-id="d0e18-130">özelleştirilmiş hello `CustomAddRows` işlevi benzer şekilde iki veri kümesi kabul eder, ancak ayrıca bir Boolean takas parametresi ek bir girdi olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="d0e18-130">hello customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="d0e18-131">Merhaba takas parametresi çok ayarlarsanız**yanlış**, onu standart uygulama hello gibi hello aynı veri kümesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="d0e18-131">If hello swap parameter is set too**FALSE**, it returns hello same data set as hello standard implementation.</span></span> <span data-ttu-id="d0e18-132">Ancak hello takas parametresi ise **doğru**, hello işlevi hello ikinci veri kümesi ilk girdi veri kümesi toohello sonuna satır yerine ekler.</span><span class="sxs-lookup"><span data-stu-id="d0e18-132">But if hello swap parameter is **TRUE**, hello function appends rows of first input dataset toohello end of hello second dataset instead.</span></span> <span data-ttu-id="d0e18-133">Merhaba R hello uyarlamasını içeren hello CustomAddRows.R dosyası `CustomAddRows` hello tarafından kullanıma sunulan işlevi **özel Add Rows** modül R koddan hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-133">hello CustomAddRows.R file that contains hello implementation of hello R `CustomAddRows` function exposed by hello **Custom Add Rows** module has hello following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a><span data-ttu-id="d0e18-134">Merhaba XML tanım dosyası</span><span class="sxs-lookup"><span data-stu-id="d0e18-134">hello XML definition file</span></span>
<span data-ttu-id="d0e18-135">tooexpose bu `CustomAddRows` toospecify işlevi bir Azure Machine Learning modülü, bir XML tanım dosyası olarak oluşturulan nasıl hello **özel Add Rows** modülü görünüş ve davranışı aynıdır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-135">tooexpose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created toospecify how hello **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="d0e18-136">Merhaba değerini hello kritik toonote olan **kimliği** hello özniteliklerini **giriş** ve **Arg** hello XML dosyasındaki öğeleri hello R hello işlevi parametre adları eşleşmelidir Merhaba CustomAddRows.R dosyasında tam olarak kod: (*dataset1*, *dataset2*, ve *takas* hello örnekte).</span><span class="sxs-lookup"><span data-stu-id="d0e18-136">It is critical toonote that hello value of hello **id** attributes of hello **Input** and **Arg** elements in hello XML file must match hello function parameter names of hello R code in hello CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in hello example).</span></span> <span data-ttu-id="d0e18-137">Benzer şekilde, hello değerini hello **entryPoint** hello özniteliği **dil** öğesi eşleşmelidir hello R betiği hello işlevinde hello adı: (*CustomAddRows* Merhaba örnekte).</span><span class="sxs-lookup"><span data-stu-id="d0e18-137">Similarly, hello value of hello **entryPoint** attribute of hello **Language** element must match hello name of hello function in hello R script EXACTLY: (*CustomAddRows* in hello example).</span></span> 

<span data-ttu-id="d0e18-138">Buna karşılık, hello **kimliği** özniteliği hello için **çıkış** öğesi hello R betiği tooany değişkenleri karşılık gelmiyor.</span><span class="sxs-lookup"><span data-stu-id="d0e18-138">In contrast, hello **id** attribute for hello **Output** element does not correspond tooany variables in hello R script.</span></span> <span data-ttu-id="d0e18-139">Birden fazla çıkış gerekli olduğunda, bir liste yerleştirilen sonuçlarıyla hello R işlevinden yalnızca dönmek *hello de aynı sırada* olarak **çıkışları** öğeleri hello XML dosyasında bildirilen.</span><span class="sxs-lookup"><span data-stu-id="d0e18-139">When more than one output is required, simply return a list from hello R function with results placed *in hello same order* as **Outputs** elements are declared in hello XML file.</span></span>

### <a name="package-and-register-hello-module"></a><span data-ttu-id="d0e18-140">Paket ve kayıt hello Modülü</span><span class="sxs-lookup"><span data-stu-id="d0e18-140">Package and register hello module</span></span>
<span data-ttu-id="d0e18-141">Bu iki dosyaları olarak kaydetmeniz *CustomAddRows.R* ve *CustomAddRows.xml* ve ardından zip hello iki dosya birlikte içine bir *CustomAddRows.zip* dosya.</span><span class="sxs-lookup"><span data-stu-id="d0e18-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip hello two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="d0e18-142">Merhaba, Machine Learning çalışma alanına gidin tooyour çalışma alanında hello Machine Learning Studio, bunları tıklatın tooregister **+ yeni** hello alta düğmesini tıklatın ve seçin **MODÜL ZIP PAKETİNİ gelen ->** tooupload Merhaba yeni **özel Add Rows** modülü.</span><span class="sxs-lookup"><span data-stu-id="d0e18-142">tooregister them in your Machine Learning workspace, go tooyour workspace in hello Machine Learning Studio, click hello **+NEW** button on hello bottom and choose **MODULE -> FROM ZIP PACKAGE** tooupload hello new **Custom Add Rows** module.</span></span>

![Zip karşıya yükle](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="d0e18-144">Merhaba **özel Add Rows** modülüdür şimdi, Machine Learning denemelerini tarafından erişilen hazır toobe.</span><span class="sxs-lookup"><span data-stu-id="d0e18-144">hello **Custom Add Rows** module is now ready toobe accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-hello-xml-definition-file"></a><span data-ttu-id="d0e18-145">Merhaba XML tanım dosyasını öğeleri</span><span class="sxs-lookup"><span data-stu-id="d0e18-145">Elements in hello XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="d0e18-146">Modül öğeleri</span><span class="sxs-lookup"><span data-stu-id="d0e18-146">Module elements</span></span>
<span data-ttu-id="d0e18-147">Merhaba **Modülü** kullanılan toodefine hello XML dosyasında özel bir modülü bir öğedir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-147">hello **Module** element is used toodefine a custom module in hello XML file.</span></span> <span data-ttu-id="d0e18-148">Birden fazla modülü birden çok kullanarak bir XML dosyasında tanımlanabilir **Modülü** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="d0e18-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="d0e18-149">Her modül çalışma alanınızda benzersiz bir ad olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="d0e18-150">Özel bir modülü aynı var olan bir özel modül adı hello kaydetme ve hello ile yeni bir hello var olan bir modül değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-150">Register a custom module with hello same name as an existing custom module and it replaces hello existing module with hello new one.</span></span> <span data-ttu-id="d0e18-151">Özel modüller ancak olabilir aynı adı var olan bir Azure Machine Learning modül hello kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="d0e18-151">Custom modules can, however, be registered with hello same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="d0e18-152">Bu nedenle, hello görünüyorsa **özel** hello modül paleti kategorisi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-152">If so, they appear in hello **Custom** category of hello module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


<span data-ttu-id="d0e18-153">Merhaba içinde **Modülü** öğesi, iki ek isteğe bağlı öğeleri belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0e18-153">Within hello **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="d0e18-154">bir **sahibi** hello modüle katıştırılmış öğesi</span><span class="sxs-lookup"><span data-stu-id="d0e18-154">an **Owner** element that is embedded into hello module</span></span>  
* <span data-ttu-id="d0e18-155">bir **açıklama** hello modülü için hızlı Yardımı'nda görüntülenir ve hello Machine Learning UI hello modülünde üzerine getirdiğinizde metni içeren öğe.</span><span class="sxs-lookup"><span data-stu-id="d0e18-155">a **Description** element that contains text that is displayed in quick help for hello module and when you hover over hello module in hello Machine Learning UI.</span></span>

<span data-ttu-id="d0e18-156">Kuralları hello modülü öğelerinde karakter sınırları için:</span><span class="sxs-lookup"><span data-stu-id="d0e18-156">Rules for characters limits in hello Module elements:</span></span>

* <span data-ttu-id="d0e18-157">Merhaba hello değerini **adı** hello özniteliğinde **Modülü** öğesi uzunluğu 64 karakteri aşmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-157">hello value of hello **name** attribute in hello **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="d0e18-158">Merhaba Merhaba içeriğine **açıklama** öğesi 128 karakterden uzun olamaz.</span><span class="sxs-lookup"><span data-stu-id="d0e18-158">hello content of hello **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="d0e18-159">Merhaba Merhaba içeriğine **sahibi** öğesi 32 karakterden uzun olamaz.</span><span class="sxs-lookup"><span data-stu-id="d0e18-159">hello content of hello **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="d0e18-160">Bir modülün sonuçları belirleyici olabilir veya nondeterministic.* * varsayılan olarak tüm modüllerin toobe belirleyici olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered toobe deterministic.</span></span> <span data-ttu-id="d0e18-161">Diğer bir deyişle, değişmeyen dizi giriş parametreleri ve verileri verildiğinde, hello modülü aynı eacRAND veya bir functionh çalıştırıldığında sonuçları hello döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-161">That is, given an unchanging set of input parameters and data, hello module should return hello same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="d0e18-162">Bu davranış verildiğinde, Azure Machine Learning Studio, bir parametre değilse belirleyici olarak işaretlenmiş Modüller yalnızca yeniden çalıştırır veya hello giriş verileri değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or hello input data has changed.</span></span> <span data-ttu-id="d0e18-163">Merhaba önbelleğe alınan sonuçları döndüren çok daha hızlı denemeler yürütülmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0e18-163">Returning hello cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="d0e18-164">RAND veya hello geçerli tarih veya saat döndüren bir işlev gibi belirleyici işlevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-164">There are functions that are nondeterministic, such as RAND or a function that returns hello current date or time.</span></span> <span data-ttu-id="d0e18-165">Modülünüzün belirleyici olmayan bir işlev kullanıyorsa, bu hello modül ayarı hello tarafından isteğe bağlı belirleyici belirtebilirsiniz **IsDeterministic** çok öznitelik**FALSE**.</span><span class="sxs-lookup"><span data-stu-id="d0e18-165">If your module uses a nondeterministic function, you can specify that hello module is non-deterministic by setting hello optional **isDeterministic** attribute too**FALSE**.</span></span> <span data-ttu-id="d0e18-166">Bu, her hello deneme çalıştırdığınızda, hello modül girişi ve parametreleri değişip değişmediğini olsa bile bu hello modülü yeniden çalıştırılır oluşturmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0e18-166">This insures that hello module is rerun whenever hello experiment is run, even if hello module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="d0e18-167">Dil tanımı</span><span class="sxs-lookup"><span data-stu-id="d0e18-167">Language Definition</span></span>
<span data-ttu-id="d0e18-168">Merhaba **dil** XML tanım dosyasını öğedir kullanılan toospecify hello özel modülü dili.</span><span class="sxs-lookup"><span data-stu-id="d0e18-168">hello **Language** element in your XML definition file is used toospecify hello custom module language.</span></span> <span data-ttu-id="d0e18-169">Şu anda, R hello yalnızca desteklenen dil değil.</span><span class="sxs-lookup"><span data-stu-id="d0e18-169">Currently, R is hello only supported language.</span></span> <span data-ttu-id="d0e18-170">Merhaba hello değerini **sourceFile** özniteliği hello işlevi toocall hello modülü çalıştırdığınızda içeren hello R dosyasının hello adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-170">hello value of hello **sourceFile** attribute must be hello name of hello R file that contains hello function toocall when hello module is run.</span></span> <span data-ttu-id="d0e18-171">Bu dosya hello zip paketinin bir parçası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-171">This file must be part of hello zip package.</span></span> <span data-ttu-id="d0e18-172">Merhaba hello değerini **entryPoint** özniteliği çağrılan hello işlevi hello adıdır ve hello kaynak dosyasında tanımlanmış geçerli bir işlev eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-172">hello value of hello **entryPoint** attribute is hello name of hello function being called and must match a valid function defined with in hello source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="d0e18-173">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="d0e18-173">Ports</span></span>
<span data-ttu-id="d0e18-174">Merhaba özel bir modülü için giriş ve çıkış bağlantı noktalarını hello alt öğelerinde belirtilen **bağlantı noktalarını** hello XML tanım dosyasını bölümü.</span><span class="sxs-lookup"><span data-stu-id="d0e18-174">hello input and output ports for a custom module are specified in child elements of hello **Ports** section of hello XML definition file.</span></span> <span data-ttu-id="d0e18-175">Bu öğelerin sırasını Hello hello düzeni deneyimli (UX) kullanıcılar tarafından belirler.</span><span class="sxs-lookup"><span data-stu-id="d0e18-175">hello order of these elements determines hello layout experienced (UX) by users.</span></span> <span data-ttu-id="d0e18-176">Merhaba ilk alt **giriş** veya **çıkış** hello listelenen **bağlantı noktalarını** hello XML dosyasının öğesinin hello en sol giriş bağlantı noktası hello Machine Learning UX olur</span><span class="sxs-lookup"><span data-stu-id="d0e18-176">hello first child **input** or **output** listed in hello **Ports** element of hello XML file becomes hello left-most input port in hello Machine Learning UX.</span></span>
<span data-ttu-id="d0e18-177">Her giriş ve çıkış bağlantı noktasına isteğe sahip **açıklama** hello Machine Learning UI hello bağlantı noktası üzerinden hello fare imlecini getirdiğinizde gösterilen hello metin belirtir alt öğesi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-177">Each input and output port may have an optional **Description** child element that specifies hello text shown when you hover hello mouse cursor over hello port in hello Machine Learning UI.</span></span>

<span data-ttu-id="d0e18-178">**Bağlantı noktası kuralları**:</span><span class="sxs-lookup"><span data-stu-id="d0e18-178">**Ports Rules**:</span></span>

* <span data-ttu-id="d0e18-179">En fazla **giriş ve çıkış bağlantı noktaları** her biri için 8'dir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="d0e18-180">Giriş öğeleri</span><span class="sxs-lookup"><span data-stu-id="d0e18-180">Input elements</span></span>
<span data-ttu-id="d0e18-181">Giriş bağlantı noktaları toopass veri tooyour R işlevi ve çalışma izin verir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-181">Input ports allow you toopass data tooyour R function and workspace.</span></span> <span data-ttu-id="d0e18-182">Merhaba **veri türleri** giriş bağlantı noktaları gibi için desteklenir:</span><span class="sxs-lookup"><span data-stu-id="d0e18-182">hello **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="d0e18-183">**DataTable:** bu tür tooyour R işlevi data.frame geçirilir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-183">**DataTable:** This type is passed tooyour R function as a data.frame.</span></span> <span data-ttu-id="d0e18-184">Aslında, Machine Learning ve, tarafından desteklenen tüm türleri (örneğin, CSV dosyalarını veya ARFF dosyaları) ile uyumlu **DataTable** dönüştürülmüş tooa data.frame otomatik olarak olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d0e18-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted tooa data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="d0e18-185">Merhaba **kimliği** her ilişkilendirilmiş özniteliği **DataTable** giriş bağlantı noktası benzersiz bir değer olmalıdır ve bu değer, R işlevi parametresinde belirtilen ilgili eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-185">hello **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="d0e18-186">İsteğe bağlı **DataTable** Giriş bir deney olarak geçmedi bağlantı noktalarını hello değere sahip **NULL** geçirilen toohello R işlev ve isteğe bağlı zip bağlantı noktalarını hello giriş bağlı değilse yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-186">Optional **DataTable** ports that are not passed as input in an experiment have hello value **NULL** passed toohello R function and optional zip ports are ignored if hello input is not connected.</span></span> <span data-ttu-id="d0e18-187">Merhaba **isteğe bağlıdır** özniteliktir hem hello için isteğe bağlı **DataTable** ve **Zip** türleri ve olduğu *false* varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="d0e18-187">hello **isOptional** attribute is optional for both hello **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="d0e18-188">**Zip:** özel modüller bir zip dosyası giriş olarak kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="d0e18-189">Bu giriş hello R çalışma dizinini işlevinizin açılmış</span><span class="sxs-lookup"><span data-stu-id="d0e18-189">This input is unpacked into hello R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

<span data-ttu-id="d0e18-190">Özel R modülleri için bir Zip bağlantı noktası için hello kimliği toomatch hello R işlevinin herhangi bir parametre yok.</span><span class="sxs-lookup"><span data-stu-id="d0e18-190">For custom R modules, hello id for a Zip port does not have toomatch any parameters of hello R function.</span></span> <span data-ttu-id="d0e18-191">Merhaba zip dosyası otomatik olarak ayıklanan toohello R çalışma dizini olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-191">This is because hello zip file is automatically extracted toohello R working directory.</span></span>

<span data-ttu-id="d0e18-192">**Giriş kuralları:**</span><span class="sxs-lookup"><span data-stu-id="d0e18-192">**Input Rules:**</span></span>

* <span data-ttu-id="d0e18-193">Merhaba hello değerini **kimliği** hello özniteliği **giriş** öğesi geçerli bir R değişken adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-193">hello value of hello **id** attribute of hello **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="d0e18-194">Merhaba hello değerini **kimliği** hello özniteliği **giriş** öğesi 64 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-194">hello value of hello **id** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="d0e18-195">Merhaba hello değerini **adı** hello özniteliği **giriş** öğesi 64 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-195">hello value of hello **name** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="d0e18-196">Merhaba Merhaba içeriğine **açıklama** öğesi 128 karakterden uzun olmamalıdır</span><span class="sxs-lookup"><span data-stu-id="d0e18-196">hello content of hello **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="d0e18-197">Merhaba hello değerini **türü** hello özniteliği **giriş** öğesi olmalıdır *Zip* veya *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="d0e18-197">hello value of hello **type** attribute of hello **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="d0e18-198">Merhaba hello değerini **isteğe bağlıdır** hello özniteliği **giriş** öğesi gerekli değildir (ve *false* belirtilmemişse varsayılan olarak); ancak belirtilirse, olmalıdır*true* veya *false*.</span><span class="sxs-lookup"><span data-stu-id="d0e18-198">hello value of hello **isOptional** attribute of hello **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="d0e18-199">Çıktı öğeleri</span><span class="sxs-lookup"><span data-stu-id="d0e18-199">Output elements</span></span>
<span data-ttu-id="d0e18-200">**Standart çıktı bağlantı noktaları:** çıkış bağlantı noktaları ardından sonraki modülleri tarafından kullanılan, R işlevi dönüş değerleri eşlenen toohello olduğunu.</span><span class="sxs-lookup"><span data-stu-id="d0e18-200">**Standard output ports:** Output ports are mapped toohello return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="d0e18-201">*DataTable* hello yalnızca standart çıkış bağlantı noktasına türü şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d0e18-201">*DataTable* is hello only standard output port type supported currently.</span></span> <span data-ttu-id="d0e18-202">(Desteği *Öğrencileriyle* ve *dönüştüren* gelecek olan.) A *DataTable* çıktı olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d0e18-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="d0e18-203">Özel R modülleri çıktılarında için başlangıç değerini hello **kimliği** özniteliğinde hello R betiği toocorrespond ile herhangi bir şey yok ancak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-203">For outputs in custom R modules, hello value of hello **id** attribute does not have toocorrespond with anything in hello R script, but it must be unique.</span></span> <span data-ttu-id="d0e18-204">Tek modülü çıktı için hello dönüş değeri hello R işlevden olmalıdır bir *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="d0e18-204">For a single module output, hello return value from hello R function must be a *data.frame*.</span></span> <span data-ttu-id="d0e18-205">Desteklenen veri türünde birden fazla nesne toooutput sipariş, hello XML tanım dosyasında belirtilen toobe hello uygun çıkış bağlantı noktaları gerekir ve bir liste olarak döndürülen toobe hello nesnelerin gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-205">In order toooutput more than one object of a supported data type, hello appropriate output ports need toobe specified in hello XML definition file and hello objects need toobe returned as a list.</span></span> <span data-ttu-id="d0e18-206">Merhaba çıkış nesnelerini toooutput bağlantı noktalarını hello nesneleri listesi döndürdü hello yerleştirilir hello sipariş yansıtma sol tooright atanır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-206">hello output objects are assigned toooutput ports from left tooright, reflecting hello order in which hello objects are placed in hello returned list.</span></span>

<span data-ttu-id="d0e18-207">Toomodify hello isterseniz, örneğin, **özel Add Rows** modülü toooutput hello özgün iki veri kümesi, *dataset1* ve *dataset2*, ayrıca toohello yeni alanına katılmış veri kümesi, *dataset*, (sol tooright ile bir sırada olarak: *dataset*, *dataset1*, *dataset2*), hello tanımlayın aşağıdaki gibi çıkış bağlantı noktasına hello CustomAddRows.xml dosyasında:</span><span class="sxs-lookup"><span data-stu-id="d0e18-207">For example, if you want toomodify hello **Custom Add Rows** module toooutput hello original two datasets, *dataset1* and *dataset2*, in addition toohello new joined dataset, *dataset*, (in an order, from left tooright, as: *dataset*, *dataset1*, *dataset2*), then define hello output ports in hello CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="d0e18-208">Ve 'CustomAddRows.R' hello doğru sırayla bir listedeki hello nesnelerinin listesini döndürür:</span><span class="sxs-lookup"><span data-stu-id="d0e18-208">And return hello list of objects in a list in hello correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="d0e18-209">**Görselleştirme çıktı:** türü bir çıkış bağlantı noktasına da belirtebilirsiniz *görselleştirme*, hello R grafik cihaz ve konsol çıkışını hello çıkış görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d0e18-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays hello output from hello R graphics device and console output.</span></span> <span data-ttu-id="d0e18-210">Bu bağlantı noktası hello R işlevi çıktı parçası olmayan ve hello diğer hello siparişle etkilemediğinden çıkış bağlantı noktası türleri.</span><span class="sxs-lookup"><span data-stu-id="d0e18-210">This port is not part of hello R function output and does not interfere with hello order of hello other output port types.</span></span> <span data-ttu-id="d0e18-211">bir görselleştirme bağlantı noktası toohello özel modüller, tooadd eklemek bir **çıkış** değerini bir öğesiyle *görselleştirme* için kendi **türü** özniteliği:</span><span class="sxs-lookup"><span data-stu-id="d0e18-211">tooadd a visualization port toohello custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

<span data-ttu-id="d0e18-212">**Çıkış kuralları:**</span><span class="sxs-lookup"><span data-stu-id="d0e18-212">**Output Rules:**</span></span>

* <span data-ttu-id="d0e18-213">Merhaba hello değerini **kimliği** hello özniteliği **çıkış** öğesi geçerli bir R değişken adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-213">hello value of hello **id** attribute of hello **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="d0e18-214">Merhaba hello değerini **kimliği** hello özniteliği **çıkış** öğesi 32 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-214">hello value of hello **id** attribute of hello **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="d0e18-215">Merhaba hello değerini **adı** hello özniteliği **çıkış** öğesi 64 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-215">hello value of hello **name** attribute of hello **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="d0e18-216">Merhaba hello değerini **türü** hello özniteliği **çıkış** öğesi olmalıdır *görselleştirme*.</span><span class="sxs-lookup"><span data-stu-id="d0e18-216">hello value of hello **type** attribute of hello **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="d0e18-217">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="d0e18-217">Arguments</span></span>
<span data-ttu-id="d0e18-218">Ek veri hello tanımlanan modülü parametreleri aracılığıyla toohello R işlevi geçirilebilir **bağımsız değişkenleri** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-218">Additional data can be passed toohello R function via module parameters which are defined in hello **Arguments** element.</span></span> <span data-ttu-id="d0e18-219">Merhaba modül seçildiğinde bu parametreler'hello Machine Learning UI hello en sağdaki Özellikler bölmesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-219">These parameters appear in hello rightmost properties pane of hello Machine Learning UI when hello module is selected.</span></span> <span data-ttu-id="d0e18-220">Bağımsız değişkenler desteklenen hello türlerinden herhangi birinde olabilir veya gerekli olduğunda özel bir numaralandırma oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0e18-220">Arguments can be any of hello supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="d0e18-221">Benzer toohello **bağlantı noktalarını** öğeleri **bağımsız değişkenleri** öğeleri isteğe bağlı bir olabilir **açıklama** hello fare geldiğinizde görüntülenen hello metnini belirtir öğesi Hello parametre adı.</span><span class="sxs-lookup"><span data-stu-id="d0e18-221">Similar toohello **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies hello text that appears when you hover hello mouse over hello parameter name.</span></span>
<span data-ttu-id="d0e18-222">DefaultValue, minValue ve maxValue gibi bir modül için isteğe bağlı özellikler tooa öznitelikleri gibi tooany bağımsız değişkeni eklenebilir **özellikleri** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added tooany argument as attributes tooa **Properties** element.</span></span> <span data-ttu-id="d0e18-223">Merhaba geçerli özelliklerini **özellikleri** öğesi hello bağımsız değişkeni türüne bağlıdır ve desteklenen hello bağımsız değişken türleriyle hello sonraki bölümde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-223">Valid properties for hello **Properties** element depend on hello argument type and are described with hello supported argument types in hello next section.</span></span> <span data-ttu-id="d0e18-224">Merhaba değişkenleriyle **isteğe bağlıdır** çok ayarlanan özelliği**"true"** hello kullanıcı tooenter bir değer gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="d0e18-224">Arguments with hello **isOptional** property set too**"true"** do not require hello user tooenter a value.</span></span> <span data-ttu-id="d0e18-225">Bir değer toohello bağımsız değişkeni sağlanmazsa, hello bağımsız değişkeni toohello giriş noktası işlevi aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="d0e18-225">If a value is not provided toohello argument, then hello argument is not passed toohello entry point function.</span></span> <span data-ttu-id="d0e18-226">İsteğe bağlı gerek toobe açıkça hello işlevi tarafından işlenmiş olan bağımsız değişkenler hello giriş noktası işlevi, örneğin varsayılan değeri NULL hello giriş noktası işlevi tanımında atanır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-226">Arguments of hello entry point function that are optional need toobe explicitly handled by hello function, e.g. assigned a default value of NULL in hello entry point function definition.</span></span> <span data-ttu-id="d0e18-227">İsteğe bağlı bir bağımsız değişken yalnızca zorunlu kılacak bir değer hello kullanıcı tarafından sağlanıyorsa diğer bağımsız değişkeni kısıtlamaları, yani min veya Mak hello.</span><span class="sxs-lookup"><span data-stu-id="d0e18-227">An optional argument will only enforce hello other argument constraints, i.e. min or max, if a value is provided by hello user.</span></span>
<span data-ttu-id="d0e18-228">Girişleri ve çıkışları'te olduğu gibi her hello parametrelerinin kendileriyle ilişkilendirilmiş benzersiz kimliği değerlere sahip önemlidir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-228">As with inputs and outputs, it is critical that each of hello parameters have unique id values associated with them.</span></span> <span data-ttu-id="d0e18-229">Bizim hızlı başlangıç örnek hello kimliği/parametre ilişkili olduğu *takas*.</span><span class="sxs-lookup"><span data-stu-id="d0e18-229">In our quick start example hello associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="d0e18-230">Arg öğesi</span><span class="sxs-lookup"><span data-stu-id="d0e18-230">Arg element</span></span>
<span data-ttu-id="d0e18-231">Hello kullanarak bir modülü parametresi tanımlı **Arg** hello alt öğesi **bağımsız değişkenleri** hello XML tanım dosyasını bölümü.</span><span class="sxs-lookup"><span data-stu-id="d0e18-231">A module parameter is defined using hello **Arg** child element of hello **Arguments** section of hello XML definition file.</span></span> <span data-ttu-id="d0e18-232">Merhaba hello alt öğe ile **bağlantı noktalarını** bölümünde, hello parametrelerinde sıralamasını hello **bağımsız değişkenleri** bölümü hello UX karşılaştı hello düzeni tanımlar</span><span class="sxs-lookup"><span data-stu-id="d0e18-232">As with hello child elements in hello **Ports** section, hello ordering of parameters in hello **Arguments** section defines hello layout encountered in hello UX.</span></span> <span data-ttu-id="d0e18-233">Merhaba parametreleri üstten aşağı aynı sipariş, bunlar tanımlanır içinde hello hello UI görünür hello XML dosyasında.</span><span class="sxs-lookup"><span data-stu-id="d0e18-233">hello parameters appear from top down in hello UI in hello same order in which they are defined in hello XML file.</span></span> <span data-ttu-id="d0e18-234">Parametreler için makine öğrenme tarafından desteklenen hello türleri burada listelenir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-234">hello types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="d0e18-235">**int** – bir tamsayı (32 bit) tür parametresi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="d0e18-236">*İsteğe bağlı özellikler*: **min**, **max**, **varsayılan** ve **isteğe bağlıdır**</span><span class="sxs-lookup"><span data-stu-id="d0e18-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="d0e18-237">**çift** – çift tür parametresi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="d0e18-238">*İsteğe bağlı özellikler*: **min**, **max**, **varsayılan** ve **isteğe bağlıdır**</span><span class="sxs-lookup"><span data-stu-id="d0e18-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="d0e18-239">**bool** – UX kutusunda onay tarafından temsil edilen bir Boolean parametresiyle</span><span class="sxs-lookup"><span data-stu-id="d0e18-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="d0e18-240">*İsteğe bağlı özellikler*: **varsayılan** -false ise ayarlanmadı</span><span class="sxs-lookup"><span data-stu-id="d0e18-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="d0e18-241">**dize**: standart bir dize</span><span class="sxs-lookup"><span data-stu-id="d0e18-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="d0e18-242">*İsteğe bağlı özellikler*: **varsayılan** ve **isteğe bağlıdır**</span><span class="sxs-lookup"><span data-stu-id="d0e18-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="d0e18-243">**ColumnPicker**: sütun seçimi parametresi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="d0e18-244">Bu tür hello UX Sütun Seçici işler.</span><span class="sxs-lookup"><span data-stu-id="d0e18-244">This type renders in hello UX as a column chooser.</span></span> <span data-ttu-id="d0e18-245">Merhaba **özelliği** öğesidir kullanılan burada toospecify hello kimliği içinden sütun seçildi, burada hello hedef bağlantı noktası türü olmalıdır hello noktasının *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="d0e18-245">hello **Property** element is used here toospecify hello id of hello port from which columns are selected, where hello target port type must be *DataTable*.</span></span> <span data-ttu-id="d0e18-246">Merhaba sütun seçimi Hello sonucunu toohello R işlevi seçili hello sütun adlarını içeren bir dize listesi olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-246">hello result of hello column selection is passed toohello R function as a list of strings containing hello selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="d0e18-247">*Özellikler gerekli*: **portId** -eşleşme türü ile bir giriş öğesinin kimliği hello *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="d0e18-247">*Required Properties*: **portId** - matches hello id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="d0e18-248">*İsteğe bağlı özellikler*:</span><span class="sxs-lookup"><span data-stu-id="d0e18-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="d0e18-249">**allowedTypes** -filtreleri hello sütun türleri hangi, seçebilirsiniz gelen.</span><span class="sxs-lookup"><span data-stu-id="d0e18-249">**allowedTypes** - Filters hello column types from which you can pick.</span></span> <span data-ttu-id="d0e18-250">Geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d0e18-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="d0e18-251">sayısal</span><span class="sxs-lookup"><span data-stu-id="d0e18-251">Numeric</span></span>
    * <span data-ttu-id="d0e18-252">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="d0e18-252">Boolean</span></span>
    * <span data-ttu-id="d0e18-253">Kategorik</span><span class="sxs-lookup"><span data-stu-id="d0e18-253">Categorical</span></span>
    * <span data-ttu-id="d0e18-254">Dize</span><span class="sxs-lookup"><span data-stu-id="d0e18-254">String</span></span>
    * <span data-ttu-id="d0e18-255">Etiket</span><span class="sxs-lookup"><span data-stu-id="d0e18-255">Label</span></span>
    * <span data-ttu-id="d0e18-256">Özellik</span><span class="sxs-lookup"><span data-stu-id="d0e18-256">Feature</span></span>
    * <span data-ttu-id="d0e18-257">Puan</span><span class="sxs-lookup"><span data-stu-id="d0e18-257">Score</span></span>
    * <span data-ttu-id="d0e18-258">Tümü</span><span class="sxs-lookup"><span data-stu-id="d0e18-258">All</span></span>
  * <span data-ttu-id="d0e18-259">**Varsayılan** -hello Sütun Seçici için geçerli varsayılan seçimleri içerir:</span><span class="sxs-lookup"><span data-stu-id="d0e18-259">**default** - Valid default selections for hello column picker include:</span></span> 
    
    * <span data-ttu-id="d0e18-260">None</span><span class="sxs-lookup"><span data-stu-id="d0e18-260">None</span></span>
    * <span data-ttu-id="d0e18-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="d0e18-261">NumericFeature</span></span>
    * <span data-ttu-id="d0e18-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="d0e18-262">NumericLabel</span></span>
    * <span data-ttu-id="d0e18-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="d0e18-263">NumericScore</span></span>
    * <span data-ttu-id="d0e18-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="d0e18-264">NumericAll</span></span>
    * <span data-ttu-id="d0e18-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="d0e18-265">BooleanFeature</span></span>
    * <span data-ttu-id="d0e18-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="d0e18-266">BooleanLabel</span></span>
    * <span data-ttu-id="d0e18-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="d0e18-267">BooleanScore</span></span>
    * <span data-ttu-id="d0e18-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="d0e18-268">BooleanAll</span></span>
    * <span data-ttu-id="d0e18-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="d0e18-269">CategoricalFeature</span></span>
    * <span data-ttu-id="d0e18-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="d0e18-270">CategoricalLabel</span></span>
    * <span data-ttu-id="d0e18-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="d0e18-271">CategoricalScore</span></span>
    * <span data-ttu-id="d0e18-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="d0e18-272">CategoricalAll</span></span>
    * <span data-ttu-id="d0e18-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="d0e18-273">StringFeature</span></span>
    * <span data-ttu-id="d0e18-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="d0e18-274">StringLabel</span></span>
    * <span data-ttu-id="d0e18-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="d0e18-275">StringScore</span></span>
    * <span data-ttu-id="d0e18-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="d0e18-276">StringAll</span></span>
    * <span data-ttu-id="d0e18-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="d0e18-277">AllLabel</span></span>
    * <span data-ttu-id="d0e18-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="d0e18-278">AllFeature</span></span>
    * <span data-ttu-id="d0e18-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="d0e18-279">AllScore</span></span>
    * <span data-ttu-id="d0e18-280">Tümü</span><span class="sxs-lookup"><span data-stu-id="d0e18-280">All</span></span>

<span data-ttu-id="d0e18-281">**Aşağı açılan**: bir kullanıcı tarafından belirtilen Enum (açılan) listesi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="d0e18-282">Merhaba açılır öğeleri hello içinde belirtilen **özellikleri** öğesini kullanarak bir **öğesi** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d0e18-282">hello dropdown items are specified within hello **Properties** element using an **Item** element.</span></span> <span data-ttu-id="d0e18-283">Merhaba **kimliği** her **öğesi** benzersiz olmalıdır ve geçerli bir R değişken.</span><span class="sxs-lookup"><span data-stu-id="d0e18-283">hello **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="d0e18-284">Merhaba hello değerini **adı** , bir **öğesi** gördüğünüz hello metin ve toohello R işlevi geçirilen hello değer görev yapar.</span><span class="sxs-lookup"><span data-stu-id="d0e18-284">hello value of hello **name** of an **Item** serves as both hello text that you see and hello value that is passed toohello R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="d0e18-285">*İsteğe bağlı özellikler*:</span><span class="sxs-lookup"><span data-stu-id="d0e18-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="d0e18-286">**Varsayılan** - hello hello varsayılan özellik hello birinden bir ID değeriyle eşleşmelidir için bir değer **öğesi** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="d0e18-286">**default** - hello value for hello default property must correspond with an id value from one of hello **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="d0e18-287">Yardımcı dosyalar</span><span class="sxs-lookup"><span data-stu-id="d0e18-287">Auxiliary Files</span></span>
<span data-ttu-id="d0e18-288">Özel Modül ZIP dosyasında yerleştirilen herhangi giderek toobe kullanılabilir yürütme sırasında bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="d0e18-288">Any file that is placed in your custom module ZIP file is going toobe available for use during execution time.</span></span> <span data-ttu-id="d0e18-289">Mevcut herhangi bir dizin yapıları korunur.</span><span class="sxs-lookup"><span data-stu-id="d0e18-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="d0e18-290">Bu, yerel olarak ve Azure Machine Learning yürütme hello dosya kaynak belirleme çalışır, aynı satırları yerine olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d0e18-290">This means that file sourcing works hello same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="d0e18-291">Tüm dosyaları ayıklanan too'src olduğunu fark ' tüm yola sahip olmanız gerekir böylece dizin ' src /' öneki.</span><span class="sxs-lookup"><span data-stu-id="d0e18-291">Notice that all files are extracted too‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="d0e18-292">Örneğin, NAs ile herhangi bir satır hello kümesinden tooremove istediğiniz ve ayrıca CustomAddRows çıktısı önce tüm yinelenen satırları kaldırır ve bir dosyada RemoveDupNARows.R yapan bir R işlevi zaten yazdıktan varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d0e18-292">For example, say you want tooremove any rows with NAs from hello dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="d0e18-293">Merhaba yardımcı dosyasında RemoveDupNARows.R hello CustomAddRows işlevi kaynak:</span><span class="sxs-lookup"><span data-stu-id="d0e18-293">You can source hello auxiliary file RemoveDupNARows.R in hello CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="d0e18-294">Ardından, 'CustomAddRows.R', 'CustomAddRows.xml' ve 'RemoveDupNARows.R' özel bir R modülü olarak içeren bir zip dosyası karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d0e18-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="d0e18-295">Yürütme Ortamı</span><span class="sxs-lookup"><span data-stu-id="d0e18-295">Execution Environment</span></span>
<span data-ttu-id="d0e18-296">Merhaba yürütme ortamı hello R betiği için kullandığı aynı R sürümde hello hello **R betiği yürütün** modülü ve Kullan'ın aynı hello varsayılan paketler.</span><span class="sxs-lookup"><span data-stu-id="d0e18-296">hello execution environment for hello R script uses hello same version of R as hello **Execute R Script** module and can use hello same default packages.</span></span> <span data-ttu-id="d0e18-297">Ek R paketleri tooyour özel modülü hello Özel Modül zip paketine ekleyerek de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0e18-297">You can also add additional R packages tooyour custom module by including them in hello custom module zip package.</span></span> <span data-ttu-id="d0e18-298">Yalnızca kendi R ortamında gibi bunları R komut dosyanıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d0e18-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="d0e18-299">**Merhaba yürütme ortamı sınırlamaları** içerir:</span><span class="sxs-lookup"><span data-stu-id="d0e18-299">**Limitations of hello execution environment** include:</span></span>

* <span data-ttu-id="d0e18-300">Kalıcı olmayan dosya sistemi: hello özel modülü çalıştırdığınızda yazılmış dosyaları hello birden çok çalıştırmaları arasında sürdürülmez aynı modülü.</span><span class="sxs-lookup"><span data-stu-id="d0e18-300">Non-persistent file system: Files written when hello custom module is run are not persisted across multiple runs of hello same module.</span></span>
* <span data-ttu-id="d0e18-301">Ağ erişim yok</span><span class="sxs-lookup"><span data-stu-id="d0e18-301">No network access</span></span>

