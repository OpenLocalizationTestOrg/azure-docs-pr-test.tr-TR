---
title: "Azure Machine learning'de özel R modülleri yazma | Microsoft Docs"
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
ms.openlocfilehash: 964ddb551a475243891abce8a2b835e65569a4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="8bd59-103">Azure Machine Learning'de özel R modülleri yazma</span><span class="sxs-lookup"><span data-stu-id="8bd59-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="8bd59-104">Bu konu, yazar ve Azure Machine learning'de özel R modülü dağıtabilirsiniz açıklar.</span><span class="sxs-lookup"><span data-stu-id="8bd59-104">This topic describes how to author and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="8bd59-105">Özel R modülleri nelerdir ve hangi dosyaların bunları tanımlamak için kullanılan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-105">It explains what custom R modules are and what files are used to define them.</span></span> <span data-ttu-id="8bd59-106">Bir modülün tanımlanması dosyaları oluşturma ve Machine Learning çalışma alanında dağıtım modülü nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-106">It illustrates how to construct the files that define a module and how to register the module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="8bd59-107">Özel modülü tanımında kullanılan öznitelikler ve öğeler daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-107">The elements and attributes used in the definition of the custom module are then described in more detail.</span></span> <span data-ttu-id="8bd59-108">Yardımcı işlevleri, dosya ve birden çok çıktıları kullanmayı da ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-108">How to use auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="8bd59-109">Özel bir R Modülü nedir?</span><span class="sxs-lookup"><span data-stu-id="8bd59-109">What is a custom R module?</span></span>
<span data-ttu-id="8bd59-110">A **özel Modülü** alanınıza yüklenebilir ve bir Azure Machine Learning deneme bir parçası olarak çalıştırılan bir kullanıcı tarafından tanımlanan modüldür.</span><span class="sxs-lookup"><span data-stu-id="8bd59-110">A **custom module** is a user-defined module that can be uploaded to your workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="8bd59-111">A **özel R Modülü** kullanıcı tanımlı bir R işlev yürüten özel bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="8bd59-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="8bd59-112">**R** istatistiksel bilgi işlem ve istatistikçiler ve veri bilimcilerine tarafından algoritmaları uygulamak için yaygın olarak kullanılan grafik için bir programlama dilidir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="8bd59-113">Şu anda R özel modüller, ancak destek ek dilleri zamanlandığı yönelik için gelecek sürümlerde desteklenen tek dilidir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-113">Currently, R is the only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="8bd59-114">Özel modüller sahip **birinci sınıf durum** Azure Machine learning'de diğer modülü gibi kullanılabilir olduğunu herkese açık.</span><span class="sxs-lookup"><span data-stu-id="8bd59-114">Custom modules have **first-class status** in Azure Machine Learning in the sense that they can be used just like any other module.</span></span> <span data-ttu-id="8bd59-115">Yayımlanan denemeler veya görselleştirmeleri dahil, diğer modüllerle çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="8bd59-116">Modül, giriş ve kullanılacak çıkış bağlantı noktaları, modelleme parametreleri ve diğer çeşitli çalışma zamanı davranışları tarafından uygulanan algoritması üzerinde denetiminiz yoktur.</span><span class="sxs-lookup"><span data-stu-id="8bd59-116">You have control over the algorithm implemented by the module, the input and output ports to be used, the modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="8bd59-117">Özel modüller içeren bir denemeyi da kolayca paylaşım Cortana Intelligence Galerisi içine yayımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-117">An experiment that contains custom modules can also be published into the Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="8bd59-118">Özel bir R Modülü dosyaları</span><span class="sxs-lookup"><span data-stu-id="8bd59-118">Files in a custom R module</span></span>
<span data-ttu-id="8bd59-119">Özel bir R modülü, en az iki dosyalarını içeren bir .zip dosyası tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8bd59-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="8bd59-120">A **kaynak dosyası** modülü tarafından kullanıma sunulan R işlevi uygular</span><span class="sxs-lookup"><span data-stu-id="8bd59-120">A **source file** that implements the R function exposed by the module</span></span>
* <span data-ttu-id="8bd59-121">Bir **XML tanım dosyasını** özel modülü arabirimi açıklar</span><span class="sxs-lookup"><span data-stu-id="8bd59-121">An **XML definition file** that describes the custom module interface</span></span>

<span data-ttu-id="8bd59-122">Ek yardımcı dosyalar da özel modülünden erişilebilir işlevselliği sağlayan .zip dosya eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-122">Additional auxiliary files can also be included in the .zip file that provides functionality that can be accessed from the custom module.</span></span> <span data-ttu-id="8bd59-123">Bu seçenek içinde ele alınmıştır **bağımsız değişkenleri** başvuru bölümünde parçası **XML tanım dosyasını öğelerinde** hızlı başlangıç örnek aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="8bd59-123">This option is discussed in the **Arguments** part of the reference section **Elements in the XML definition file** following the quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="8bd59-124">Hızlı Başlangıç örnek: tanımlamak, paket ve özel bir R modülü kaydetme</span><span class="sxs-lookup"><span data-stu-id="8bd59-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="8bd59-125">Bu örnek özel bir R modülü tarafından gerekli dosyaları oluşturmak, bir zip dosyasına paketini ve ardından modülü Machine Learning çalışma alanınızda kaydetmek nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-125">This example illustrates how to construct the files required by a custom R module, package them into a zip file, and then register the module in your Machine Learning workspace.</span></span> <span data-ttu-id="8bd59-126">Örnek zip paketini ve örnek dosyaları yüklenebilir [CustomAddRows.zip karşıdan dosya](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="8bd59-126">The example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="the-source-file"></a><span data-ttu-id="8bd59-127">Kaynak dosya</span><span class="sxs-lookup"><span data-stu-id="8bd59-127">The source file</span></span>
<span data-ttu-id="8bd59-128">Örneği göz önünde bulundurun bir **özel Add Rows** standart uygulaması değiştirir Modülü **Add Rows** satırları (gözlemleri) iki veri kümesi (veri çerçevelerini) birleştirmek için kullanılan modül.</span><span class="sxs-lookup"><span data-stu-id="8bd59-128">Consider the example of a **Custom Add Rows** module that modifies the standard implementation of the **Add Rows** module used to concatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="8bd59-129">Standart **Add Rows** modül kullanarak ilk girdi veri kümesi sonuna ikinci girdi veri kümesi satırlarını ekler `rbind` algoritması.</span><span class="sxs-lookup"><span data-stu-id="8bd59-129">The standard **Add Rows** module appends the rows of the second input dataset to the end of the first input dataset using the `rbind` algorithm.</span></span> <span data-ttu-id="8bd59-130">Özelleştirilmiş `CustomAddRows` işlevi benzer şekilde iki veri kümesi kabul eder, ancak ayrıca bir Boolean takas parametresi ek bir girdi olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="8bd59-130">The customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="8bd59-131">Takas parametresi ayarlanmışsa **yanlış**, aynı veri kümesi standart uygulaması olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="8bd59-131">If the swap parameter is set to **FALSE**, it returns the same data set as the standard implementation.</span></span> <span data-ttu-id="8bd59-132">Ancak takas parametresi ise **doğru**, bunun yerine ikinci veri kümesi sonuna işlevi ilk girdi veri kümesi satırlarını ekler.</span><span class="sxs-lookup"><span data-stu-id="8bd59-132">But if the swap parameter is **TRUE**, the function appends rows of first input dataset to the end of the second dataset instead.</span></span> <span data-ttu-id="8bd59-133">R uyarlamasını içeren CustomAddRows.R dosyası `CustomAddRows` işlevi kullanıma sunulan **özel Add Rows** Modülü aşağıdaki R kodu içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8bd59-133">The CustomAddRows.R file that contains the implementation of the R `CustomAddRows` function exposed by the **Custom Add Rows** module has the following R code.</span></span>

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

### <a name="the-xml-definition-file"></a><span data-ttu-id="8bd59-134">XML tanım dosyasını</span><span class="sxs-lookup"><span data-stu-id="8bd59-134">The XML definition file</span></span>
<span data-ttu-id="8bd59-135">Bu kullanıma sunmak için `CustomAddRows` işlevi bir Azure Machine Learning modülü, bir XML tanım dosyası olarak oluşturulan, belirtmek için nasıl **özel Add Rows** modülü görünüş ve davranışı aynıdır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-135">To expose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created to specify how the **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another. Dataset 2 is concatenated to Dataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify the base language, script file and R function to use for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: The values of the id attributes in the Input and Arg elements must match the parameter names in the R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>The combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="8bd59-136">Unutmayın önemlidir değerini **kimliği** özniteliklerini **giriş** ve **Arg** XML dosyasındaki öğeleri R kodu işlevi parametre adları eşleşmelidir CustomAddRows.R dosya tam: (*dataset1*, *dataset2*, ve *takas* örnekte).</span><span class="sxs-lookup"><span data-stu-id="8bd59-136">It is critical to note that the value of the **id** attributes of the **Input** and **Arg** elements in the XML file must match the function parameter names of the R code in the CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in the example).</span></span> <span data-ttu-id="8bd59-137">Benzer şekilde, değeri **entryPoint** özniteliği **dil** öğesi eşleşmelidir R betiği işlevinde adı: (*CustomAddRows* örnekte) .</span><span class="sxs-lookup"><span data-stu-id="8bd59-137">Similarly, the value of the **entryPoint** attribute of the **Language** element must match the name of the function in the R script EXACTLY: (*CustomAddRows* in the example).</span></span> 

<span data-ttu-id="8bd59-138">Buna karşılık, **kimliği** için öznitelik **çıkış** öğesi R betiği herhangi değişkenlerine karşılık gelmiyor.</span><span class="sxs-lookup"><span data-stu-id="8bd59-138">In contrast, the **id** attribute for the **Output** element does not correspond to any variables in the R script.</span></span> <span data-ttu-id="8bd59-139">Birden fazla çıkış gerekli olduğunda, bir liste yerleştirilen sonuçlarıyla R işlevinden yalnızca dönmek *aynı sırada* olarak **çıkışları** öğeleri XML dosyasında bildirilen.</span><span class="sxs-lookup"><span data-stu-id="8bd59-139">When more than one output is required, simply return a list from the R function with results placed *in the same order* as **Outputs** elements are declared in the XML file.</span></span>

### <a name="package-and-register-the-module"></a><span data-ttu-id="8bd59-140">Paket ve kaydetme modülü</span><span class="sxs-lookup"><span data-stu-id="8bd59-140">Package and register the module</span></span>
<span data-ttu-id="8bd59-141">Bu iki dosyaları olarak kaydetmeniz *CustomAddRows.R* ve *CustomAddRows.xml* ve ardından iki birlikte içine ZIP dosyaları bir *CustomAddRows.zip* dosya.</span><span class="sxs-lookup"><span data-stu-id="8bd59-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip the two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="8bd59-142">Machine Learning çalışma alanınızda kaydetmek için Machine Learning Studio'da çalışma alanınıza gidin, **+ yeni** alta düğmesini tıklatın ve seçin **MODÜL ZIP PAKETİNİ gelen ->** yeni karşıya yüklemek için **Özel Add Rows** modülü.</span><span class="sxs-lookup"><span data-stu-id="8bd59-142">To register them in your Machine Learning workspace, go to your workspace in the Machine Learning Studio, click the **+NEW** button on the bottom and choose **MODULE -> FROM ZIP PACKAGE** to upload the new **Custom Add Rows** module.</span></span>

![Zip karşıya yükle](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="8bd59-144">**Özel Add Rows** modülüdür şimdi, Machine Learning denemelerini tarafından erişilebilmesi hazır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-144">The **Custom Add Rows** module is now ready to be accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-the-xml-definition-file"></a><span data-ttu-id="8bd59-145">XML tanım dosyasını öğeleri</span><span class="sxs-lookup"><span data-stu-id="8bd59-145">Elements in the XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="8bd59-146">Modül öğeleri</span><span class="sxs-lookup"><span data-stu-id="8bd59-146">Module elements</span></span>
<span data-ttu-id="8bd59-147">**Modülü** öğe XML dosyasında özel bir modülü tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-147">The **Module** element is used to define a custom module in the XML file.</span></span> <span data-ttu-id="8bd59-148">Birden fazla modülü birden çok kullanarak bir XML dosyasında tanımlanabilir **Modülü** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="8bd59-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="8bd59-149">Her modül çalışma alanınızda benzersiz bir ad olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="8bd59-150">Var olan bir özel modül aynı ada sahip özel bir modülü kaydetmek ve var olan bir modül yeni bir bağlantıyla değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-150">Register a custom module with the same name as an existing custom module and it replaces the existing module with the new one.</span></span> <span data-ttu-id="8bd59-151">Özel modüller ancak olabilir var olan bir Azure Machine Learning modül adıyla aynı kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="8bd59-151">Custom modules can, however, be registered with the same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="8bd59-152">Bu nedenle, bunlar görünüyorsa **özel** modül paleti kategorisi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-152">If so, they appear in the **Custom** category of the module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another...</Description>/> 


<span data-ttu-id="8bd59-153">İçinde **Modülü** öğesi, iki ek isteğe bağlı öğeleri belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8bd59-153">Within the **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="8bd59-154">bir **sahibi** modüle katıştırılmış öğesi</span><span class="sxs-lookup"><span data-stu-id="8bd59-154">an **Owner** element that is embedded into the module</span></span>  
* <span data-ttu-id="8bd59-155">bir **açıklama** modülü için hızlı Yardımı'nda görüntülenir ve makine öğrenme UI modülünde üzerine getirdiğinizde metni içeren öğe.</span><span class="sxs-lookup"><span data-stu-id="8bd59-155">a **Description** element that contains text that is displayed in quick help for the module and when you hover over the module in the Machine Learning UI.</span></span>

<span data-ttu-id="8bd59-156">Kuralları modülü öğelerindeki karakter sınırları için:</span><span class="sxs-lookup"><span data-stu-id="8bd59-156">Rules for characters limits in the Module elements:</span></span>

* <span data-ttu-id="8bd59-157">Değeri **adı** özniteliğini **Modülü** öğesi uzunluğu 64 karakteri aşmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-157">The value of the **name** attribute in the **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="8bd59-158">İçeriği **açıklama** öğesi 128 karakterden uzun olamaz.</span><span class="sxs-lookup"><span data-stu-id="8bd59-158">The content of the **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="8bd59-159">İçeriği **sahibi** öğesi 32 karakterden uzun olamaz.</span><span class="sxs-lookup"><span data-stu-id="8bd59-159">The content of the **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="8bd59-160">Bir modülün sonuçları belirleyici olabilir veya nondeterministic.* * varsayılan olarak tüm modüllerin belirleyici olduğu kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered to be deterministic.</span></span> <span data-ttu-id="8bd59-161">Diğer bir deyişle, değişmeyen dizi giriş parametreleri ve verileri verildiğinde, modül aynı sonuçları eacRAND veya bir functionh çalıştırıldığında döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-161">That is, given an unchanging set of input parameters and data, the module should return the same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="8bd59-162">Bu davranış verildiğinde, Azure Machine Learning Studio, bir parametre değilse belirleyici olarak işaretlenmiş Modüller yalnızca yeniden çalıştırır veya giriş verileri değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or the input data has changed.</span></span> <span data-ttu-id="8bd59-163">Önbelleğe alınan sonuçları döndüren çok daha hızlı denemeler yürütülmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bd59-163">Returning the cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="8bd59-164">RAND veya geçerli tarih ve saati döndüren bir işlev gibi belirleyici işlevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-164">There are functions that are nondeterministic, such as RAND or a function that returns the current date or time.</span></span> <span data-ttu-id="8bd59-165">Modülünüzün belirleyici olmayan bir işlev kullanıyorsa, isteğe bağlı ayarlayarak modülü belirleyici olduğunu belirtebilirsiniz **IsDeterministic** özniteliğini **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="8bd59-165">If your module uses a nondeterministic function, you can specify that the module is non-deterministic by setting the optional **isDeterministic** attribute to **FALSE**.</span></span> <span data-ttu-id="8bd59-166">Bu denemeyi çalıştırın her giriş modülü ve parametreleri değişip değişmediğini olsa bile modülü yeniden çalıştırılır, yöntem başlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8bd59-166">This insures that the module is rerun whenever the experiment is run, even if the module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="8bd59-167">Dil tanımı</span><span class="sxs-lookup"><span data-stu-id="8bd59-167">Language Definition</span></span>
<span data-ttu-id="8bd59-168">**Dil** XML tanım dosyasını öğesinde özel modülü dili belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-168">The **Language** element in your XML definition file is used to specify the custom module language.</span></span> <span data-ttu-id="8bd59-169">Şu anda R yalnızca desteklenen dilidir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-169">Currently, R is the only supported language.</span></span> <span data-ttu-id="8bd59-170">Değeri **sourceFile** özniteliği modülü çalıştırdığınızda çağrılacak işlevi içeren R dosya adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-170">The value of the **sourceFile** attribute must be the name of the R file that contains the function to call when the module is run.</span></span> <span data-ttu-id="8bd59-171">Bu dosya zip paketinin bir parçası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-171">This file must be part of the zip package.</span></span> <span data-ttu-id="8bd59-172">Değeri **entryPoint** özniteliği çağrılan işlev adıdır ve kaynak dosyasında tanımlanmış geçerli bir işlev eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-172">The value of the **entryPoint** attribute is the name of the function being called and must match a valid function defined with in the source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="8bd59-173">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="8bd59-173">Ports</span></span>
<span data-ttu-id="8bd59-174">Özel bir modülü için giriş ve çıkış bağlantı noktalarını alt öğelerinin içinde belirtilen **bağlantı noktalarını** XML tanım dosyasını bölümü.</span><span class="sxs-lookup"><span data-stu-id="8bd59-174">The input and output ports for a custom module are specified in child elements of the **Ports** section of the XML definition file.</span></span> <span data-ttu-id="8bd59-175">Bu öğelerin sırasını düzeni deneyimli (UX) kullanıcılar tarafından belirler.</span><span class="sxs-lookup"><span data-stu-id="8bd59-175">The order of these elements determines the layout experienced (UX) by users.</span></span> <span data-ttu-id="8bd59-176">İlk alt **giriş** veya **çıkış** listelenen **bağlantı noktalarını** XML dosyasının öğe haline gelir, Machine Learning UX en sol giriş bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="8bd59-176">The first child **input** or **output** listed in the **Ports** element of the XML file becomes the left-most input port in the Machine Learning UX.</span></span>
<span data-ttu-id="8bd59-177">Her giriş ve çıkış bağlantı noktasına isteğe sahip **açıklama** Machine Learning arabiriminde bağlantı noktası üzerinden fare imleci getirdiğinizde gösterilen metni belirtir alt öğesi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-177">Each input and output port may have an optional **Description** child element that specifies the text shown when you hover the mouse cursor over the port in the Machine Learning UI.</span></span>

<span data-ttu-id="8bd59-178">**Bağlantı noktası kuralları**:</span><span class="sxs-lookup"><span data-stu-id="8bd59-178">**Ports Rules**:</span></span>

* <span data-ttu-id="8bd59-179">En fazla **giriş ve çıkış bağlantı noktaları** her biri için 8'dir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="8bd59-180">Giriş öğeleri</span><span class="sxs-lookup"><span data-stu-id="8bd59-180">Input elements</span></span>
<span data-ttu-id="8bd59-181">Giriş bağlantı noktaları, R işlevi ve çalışma alanı için veri iletmek izin verir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-181">Input ports allow you to pass data to your R function and workspace.</span></span> <span data-ttu-id="8bd59-182">**Veri türleri** giriş bağlantı noktaları gibi için desteklenir:</span><span class="sxs-lookup"><span data-stu-id="8bd59-182">The **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="8bd59-183">**DataTable:** bu tür R işlevinizde bir data.frame olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-183">**DataTable:** This type is passed to your R function as a data.frame.</span></span> <span data-ttu-id="8bd59-184">Aslında, Machine Learning ve, tarafından desteklenen tüm türleri (örneğin, CSV dosyalarını veya ARFF dosyaları) ile uyumlu **DataTable** data.frame için otomatik olarak dönüştürülür.</span><span class="sxs-lookup"><span data-stu-id="8bd59-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted to a data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="8bd59-185">**Kimliği** her ilişkilendirilmiş özniteliği **DataTable** giriş bağlantı noktası benzersiz bir değer olmalıdır ve bu değer, R işlevi parametresinde belirtilen ilgili eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-185">The **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="8bd59-186">İsteğe bağlı **DataTable** Giriş bir deney olarak geçmedi bağlantı noktalarının olması ve değerin **NULL** giriş bağlı değilse bağlantı noktaları göz ardı R işlev ve isteğe bağlı zip geçirildi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-186">Optional **DataTable** ports that are not passed as input in an experiment have the value **NULL** passed to the R function and optional zip ports are ignored if the input is not connected.</span></span> <span data-ttu-id="8bd59-187">**İsteğe bağlıdır** özniteliktir her ikisi için isteğe bağlı **DataTable** ve **Zip** türleri ve olduğu *false* varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="8bd59-187">The **isOptional** attribute is optional for both the **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="8bd59-188">**Zip:** özel modüller bir zip dosyası giriş olarak kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="8bd59-189">Bu giriş işlevinizi R çalışma dizinine açılmış</span><span class="sxs-lookup"><span data-stu-id="8bd59-189">This input is unpacked into the R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files to be extracted to the R working directory.</Description>
           </Input>

<span data-ttu-id="8bd59-190">Özel R modülleri için herhangi bir parametre R işlevinin eşleşecek şekilde Zip bağlantı noktası kimliği yok.</span><span class="sxs-lookup"><span data-stu-id="8bd59-190">For custom R modules, the id for a Zip port does not have to match any parameters of the R function.</span></span> <span data-ttu-id="8bd59-191">Zip dosyası otomatik olarak R çalışma dizinini ayıklanan olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-191">This is because the zip file is automatically extracted to the R working directory.</span></span>

<span data-ttu-id="8bd59-192">**Giriş kuralları:**</span><span class="sxs-lookup"><span data-stu-id="8bd59-192">**Input Rules:**</span></span>

* <span data-ttu-id="8bd59-193">Değeri **kimliği** özniteliği **giriş** öğesi geçerli bir R değişken adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-193">The value of the **id** attribute of the **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="8bd59-194">Değeri **kimliği** özniteliği **giriş** öğesi 64 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-194">The value of the **id** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="8bd59-195">Değeri **adı** özniteliği **giriş** öğesi 64 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-195">The value of the **name** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="8bd59-196">İçeriği **açıklama** öğesi 128 karakterden uzun olmamalıdır</span><span class="sxs-lookup"><span data-stu-id="8bd59-196">The content of the **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="8bd59-197">Değeri **türü** özniteliği **giriş** öğesi olmalıdır *Zip* veya *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="8bd59-197">The value of the **type** attribute of the **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="8bd59-198">Değeri **isteğe bağlıdır** özniteliği **giriş** öğesi gerekli değildir (ve *false* belirtilmemişse varsayılan olarak); ancak belirtilirse, olmalıdır*true* veya *false*.</span><span class="sxs-lookup"><span data-stu-id="8bd59-198">The value of the **isOptional** attribute of the **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="8bd59-199">Çıktı öğeleri</span><span class="sxs-lookup"><span data-stu-id="8bd59-199">Output elements</span></span>
<span data-ttu-id="8bd59-200">**Standart çıktı bağlantı noktaları:** çıkış bağlantı noktaları ardından sonraki modülleri tarafından kullanılan, R işlevinin dönüş değerleri eşlendi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-200">**Standard output ports:** Output ports are mapped to the return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="8bd59-201">*DataTable* yalnızca standart çıktı bağlantı noktası türü şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="8bd59-201">*DataTable* is the only standard output port type supported currently.</span></span> <span data-ttu-id="8bd59-202">(Desteği *Öğrencileriyle* ve *dönüştüren* gelecek olan.) A *DataTable* çıktı olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="8bd59-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="8bd59-203">Özel R modülleri, değerini çıktılarında için **kimliği** özniteliği her şeyi R betiği ile karşılık gelen gerekmez, ancak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-203">For outputs in custom R modules, the value of the **id** attribute does not have to correspond with anything in the R script, but it must be unique.</span></span> <span data-ttu-id="8bd59-204">Tek modülü çıktı için R işlevden dönüş değeri olmalıdır bir *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="8bd59-204">For a single module output, the return value from the R function must be a *data.frame*.</span></span> <span data-ttu-id="8bd59-205">Desteklenen veri türünde birden fazla nesne çıktı için uygun çıkış bağlantı noktaları XML tanım dosyasında belirtilmesi gerekir ve bir liste olarak döndürülecek nesneleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-205">In order to output more than one object of a supported data type, the appropriate output ports need to be specified in the XML definition file and the objects need to be returned as a list.</span></span> <span data-ttu-id="8bd59-206">Çıkış nesnelerini çıkış bağlantı noktasına soldan sağa nesneleri döndürülen listede yerleştirilir sipariş yansıtma atanmış.</span><span class="sxs-lookup"><span data-stu-id="8bd59-206">The output objects are assigned to output ports from left to right, reflecting the order in which the objects are placed in the returned list.</span></span>

<span data-ttu-id="8bd59-207">Örneğin, değişiklik yapmak istiyorsanız **özel satırları ekleyin** özgün iki veri kümesi çıkış modülü *dataset1* ve *dataset2*, yeni birleştirilmiş veri kümesi yanı sıra *dataset*, (soldan sağa, bir sırada olarak: *dataset*, *dataset1*, *dataset2*), çıkış bağlantı noktaları tanımlayın CustomAddRows.xml dosya şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="8bd59-207">For example, if you want to modify the **Custom Add Rows** module to output the original two datasets, *dataset1* and *dataset2*, in addition to the new joined dataset, *dataset*, (in an order, from left to right, as: *dataset*, *dataset1*, *dataset2*), then define the output ports in the CustomAddRows.xml file as follows:</span></span>

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


<span data-ttu-id="8bd59-208">Ve doğru sırada 'CustomAddRows.R' listesinde nesnelerinin listesini döndürür:</span><span class="sxs-lookup"><span data-stu-id="8bd59-208">And return the list of objects in a list in the correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="8bd59-209">**Görselleştirme çıktı:** türü bir çıkış bağlantı noktasına da belirtebilirsiniz *görselleştirme*, R grafik cihaz ve konsol çıkışını bir çıkış görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8bd59-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays the output from the R graphics device and console output.</span></span> <span data-ttu-id="8bd59-210">Bu bağlantı noktası R işlevi çıktı parçası olmayan ve bir çıkış bağlantı noktası türleri sırasını etkilemez.</span><span class="sxs-lookup"><span data-stu-id="8bd59-210">This port is not part of the R function output and does not interfere with the order of the other output port types.</span></span> <span data-ttu-id="8bd59-211">Özel modüllerle görselleştirme bağlantı noktası eklemek için Ekle bir **çıkış** değerini bir öğesiyle *görselleştirme* için kendi **türü** özniteliği:</span><span class="sxs-lookup"><span data-stu-id="8bd59-211">To add a visualization port to the custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View the R console graphics device output.</Description>
    </Output>

<span data-ttu-id="8bd59-212">**Çıkış kuralları:**</span><span class="sxs-lookup"><span data-stu-id="8bd59-212">**Output Rules:**</span></span>

* <span data-ttu-id="8bd59-213">Değeri **kimliği** özniteliği **çıkış** öğesi geçerli bir R değişken adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-213">The value of the **id** attribute of the **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="8bd59-214">Değeri **kimliği** özniteliği **çıkış** öğesi 32 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-214">The value of the **id** attribute of the **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="8bd59-215">Değeri **adı** özniteliği **çıkış** öğesi 64 karakterden uzun olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-215">The value of the **name** attribute of the **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="8bd59-216">Değeri **türü** özniteliği **çıkış** öğesi olmalıdır *görselleştirme*.</span><span class="sxs-lookup"><span data-stu-id="8bd59-216">The value of the **type** attribute of the **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="8bd59-217">Bağımsız Değişkenler</span><span class="sxs-lookup"><span data-stu-id="8bd59-217">Arguments</span></span>
<span data-ttu-id="8bd59-218">Ek veri içinde tanımlanan modülü parametreleri aracılığıyla R işleve geçirilebilir **bağımsız değişkenleri** öğesi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-218">Additional data can be passed to the R function via module parameters which are defined in the **Arguments** element.</span></span> <span data-ttu-id="8bd59-219">Modül seçildiğinde bu parametreler Machine Learning UI en sağdaki Özellikler bölmesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-219">These parameters appear in the rightmost properties pane of the Machine Learning UI when the module is selected.</span></span> <span data-ttu-id="8bd59-220">Bağımsız değişkenler desteklenen türlerinden herhangi birinde olabilir veya gerekli olduğunda özel bir numaralandırma oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd59-220">Arguments can be any of the supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="8bd59-221">Benzer şekilde **bağlantı noktaları** öğeleri **bağımsız değişkenler** öğeleri isteğe bağlı bir olabilir **açıklama** fare üzerine geldiğinizde görüntülenen metni belirtir öğesi parametre adı.</span><span class="sxs-lookup"><span data-stu-id="8bd59-221">Similar to the **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies the text that appears when you hover the mouse over the parameter name.</span></span>
<span data-ttu-id="8bd59-222">DefaultValue, minValue ve maxValue gibi bir modül için isteğe bağlı özellikler öznitelikler için olarak için herhangi bir bağımsız değişken eklenebilir bir **özellikleri** öğesi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added to any argument as attributes to a **Properties** element.</span></span> <span data-ttu-id="8bd59-223">Geçerli özelliklerini **özellikleri** öğesi bağımsız değişken türüne bağlıdır ve sonraki bölümde desteklenen bağımsız değişken türleriyle açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8bd59-223">Valid properties for the **Properties** element depend on the argument type and are described with the supported argument types in the next section.</span></span> <span data-ttu-id="8bd59-224">Bağımsız değişkenlerle **isteğe bağlıdır** özelliğini **"true"** bir değer girmesini gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="8bd59-224">Arguments with the **isOptional** property set to **"true"** do not require the user to enter a value.</span></span> <span data-ttu-id="8bd59-225">Bir değer bağımsız değişkeni sağlanmazsa, bağımsız değişkeni için giriş noktası işlevi aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="8bd59-225">If a value is not provided to the argument, then the argument is not passed to the entry point function.</span></span> <span data-ttu-id="8bd59-226">İsteğe bağlı bağımsız değişkenler giriş noktası işlevinin açıkça örneğin varsayılan değeri NULL giriş noktası işlevi tanımında atanan işlevi tarafından ele alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-226">Arguments of the entry point function that are optional need to be explicitly handled by the function, e.g. assigned a default value of NULL in the entry point function definition.</span></span> <span data-ttu-id="8bd59-227">Kullanıcı tarafından sağlanan bir değeri, isteğe bağlı bir bağımsız değişken yalnızca diğer bağımsız değişkeni kısıtlamaları, yani min veya Mak uygulayın.</span><span class="sxs-lookup"><span data-stu-id="8bd59-227">An optional argument will only enforce the other argument constraints, i.e. min or max, if a value is provided by the user.</span></span>
<span data-ttu-id="8bd59-228">Girişleri ve çıkışları'te olduğu gibi her bir parametreyi kendileriyle ilişkilendirilmiş benzersiz kimliği değerlere sahip önemlidir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-228">As with inputs and outputs, it is critical that each of the parameters have unique id values associated with them.</span></span> <span data-ttu-id="8bd59-229">Hızlı Başlangıç örneğimizde ilişkili kimliği/parametre olan *takas*.</span><span class="sxs-lookup"><span data-stu-id="8bd59-229">In our quick start example the associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="8bd59-230">Arg öğesi</span><span class="sxs-lookup"><span data-stu-id="8bd59-230">Arg element</span></span>
<span data-ttu-id="8bd59-231">Bir modül parametresi kullanılarak tanımlanan **Arg** alt öğesi olan **bağımsız değişkenleri** XML tanım dosyasını bölümü.</span><span class="sxs-lookup"><span data-stu-id="8bd59-231">A module parameter is defined using the **Arg** child element of the **Arguments** section of the XML definition file.</span></span> <span data-ttu-id="8bd59-232">Bir alt öğe ile **bağlantı noktalarını** bölümünde parametrelerinde sıralama **bağımsız değişkenleri** bölümü UX karşılaştı düzeni tanımlar</span><span class="sxs-lookup"><span data-stu-id="8bd59-232">As with the child elements in the **Ports** section, the ordering of parameters in the **Arguments** section defines the layout encountered in the UX.</span></span> <span data-ttu-id="8bd59-233">Parametreleri üstten aşağı XML dosyasında tanımlanan aynı sırada kullanıcı Arabiriminde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-233">The parameters appear from top down in the UI in the same order in which they are defined in the XML file.</span></span> <span data-ttu-id="8bd59-234">Parametreler için makine öğrenme tarafından desteklenen türleri burada listelenir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-234">The types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="8bd59-235">**int** – bir tamsayı (32 bit) tür parametresi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="8bd59-236">*İsteğe bağlı özellikler*: **min**, **max**, **varsayılan** ve **isteğe bağlıdır**</span><span class="sxs-lookup"><span data-stu-id="8bd59-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="8bd59-237">**çift** – çift tür parametresi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="8bd59-238">*İsteğe bağlı özellikler*: **min**, **max**, **varsayılan** ve **isteğe bağlıdır**</span><span class="sxs-lookup"><span data-stu-id="8bd59-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="8bd59-239">**bool** – UX kutusunda onay tarafından temsil edilen bir Boolean parametresiyle</span><span class="sxs-lookup"><span data-stu-id="8bd59-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="8bd59-240">*İsteğe bağlı özellikler*: **varsayılan** -false ise ayarlanmadı</span><span class="sxs-lookup"><span data-stu-id="8bd59-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="8bd59-241">**dize**: standart bir dize</span><span class="sxs-lookup"><span data-stu-id="8bd59-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="8bd59-242">*İsteğe bağlı özellikler*: **varsayılan** ve **isteğe bağlıdır**</span><span class="sxs-lookup"><span data-stu-id="8bd59-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="8bd59-243">**ColumnPicker**: sütun seçimi parametresi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="8bd59-244">Bu tür UX Sütun Seçici işler.</span><span class="sxs-lookup"><span data-stu-id="8bd59-244">This type renders in the UX as a column chooser.</span></span> <span data-ttu-id="8bd59-245">**Özelliği** öğesi burada içinden sütun seçildi, hedef bağlantı noktası türü burada olmalıdır bağlantı noktasının kimliğini belirtmek için kullanılır *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="8bd59-245">The **Property** element is used here to specify the id of the port from which columns are selected, where the target port type must be *DataTable*.</span></span> <span data-ttu-id="8bd59-246">Sütun Seçimi sonucunu R işlevi seçili sütun adlarını içeren bir dize listesi olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-246">The result of the column selection is passed to the R function as a list of strings containing the selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="8bd59-247">*Özellikler gerekli*: **portId** -giriş öğenin kimliği türü ile eşleşen *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="8bd59-247">*Required Properties*: **portId** - matches the id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="8bd59-248">*İsteğe bağlı özellikler*:</span><span class="sxs-lookup"><span data-stu-id="8bd59-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="8bd59-249">**allowedTypes** -sütun türleri hangi, seçebilirsiniz gelen filtreleri.</span><span class="sxs-lookup"><span data-stu-id="8bd59-249">**allowedTypes** - Filters the column types from which you can pick.</span></span> <span data-ttu-id="8bd59-250">Geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8bd59-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="8bd59-251">sayısal</span><span class="sxs-lookup"><span data-stu-id="8bd59-251">Numeric</span></span>
    * <span data-ttu-id="8bd59-252">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="8bd59-252">Boolean</span></span>
    * <span data-ttu-id="8bd59-253">Kategorik</span><span class="sxs-lookup"><span data-stu-id="8bd59-253">Categorical</span></span>
    * <span data-ttu-id="8bd59-254">Dize</span><span class="sxs-lookup"><span data-stu-id="8bd59-254">String</span></span>
    * <span data-ttu-id="8bd59-255">Etiket</span><span class="sxs-lookup"><span data-stu-id="8bd59-255">Label</span></span>
    * <span data-ttu-id="8bd59-256">Özellik</span><span class="sxs-lookup"><span data-stu-id="8bd59-256">Feature</span></span>
    * <span data-ttu-id="8bd59-257">Puan</span><span class="sxs-lookup"><span data-stu-id="8bd59-257">Score</span></span>
    * <span data-ttu-id="8bd59-258">Tümü</span><span class="sxs-lookup"><span data-stu-id="8bd59-258">All</span></span>
  * <span data-ttu-id="8bd59-259">**Varsayılan** -Sütun Seçici için geçerli varsayılan seçimleri içerir:</span><span class="sxs-lookup"><span data-stu-id="8bd59-259">**default** - Valid default selections for the column picker include:</span></span> 
    
    * <span data-ttu-id="8bd59-260">None</span><span class="sxs-lookup"><span data-stu-id="8bd59-260">None</span></span>
    * <span data-ttu-id="8bd59-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="8bd59-261">NumericFeature</span></span>
    * <span data-ttu-id="8bd59-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="8bd59-262">NumericLabel</span></span>
    * <span data-ttu-id="8bd59-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="8bd59-263">NumericScore</span></span>
    * <span data-ttu-id="8bd59-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="8bd59-264">NumericAll</span></span>
    * <span data-ttu-id="8bd59-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="8bd59-265">BooleanFeature</span></span>
    * <span data-ttu-id="8bd59-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="8bd59-266">BooleanLabel</span></span>
    * <span data-ttu-id="8bd59-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="8bd59-267">BooleanScore</span></span>
    * <span data-ttu-id="8bd59-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="8bd59-268">BooleanAll</span></span>
    * <span data-ttu-id="8bd59-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="8bd59-269">CategoricalFeature</span></span>
    * <span data-ttu-id="8bd59-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="8bd59-270">CategoricalLabel</span></span>
    * <span data-ttu-id="8bd59-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="8bd59-271">CategoricalScore</span></span>
    * <span data-ttu-id="8bd59-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="8bd59-272">CategoricalAll</span></span>
    * <span data-ttu-id="8bd59-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="8bd59-273">StringFeature</span></span>
    * <span data-ttu-id="8bd59-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="8bd59-274">StringLabel</span></span>
    * <span data-ttu-id="8bd59-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="8bd59-275">StringScore</span></span>
    * <span data-ttu-id="8bd59-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="8bd59-276">StringAll</span></span>
    * <span data-ttu-id="8bd59-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="8bd59-277">AllLabel</span></span>
    * <span data-ttu-id="8bd59-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="8bd59-278">AllFeature</span></span>
    * <span data-ttu-id="8bd59-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="8bd59-279">AllScore</span></span>
    * <span data-ttu-id="8bd59-280">Tümü</span><span class="sxs-lookup"><span data-stu-id="8bd59-280">All</span></span>

<span data-ttu-id="8bd59-281">**Aşağı açılan**: bir kullanıcı tarafından belirtilen Enum (açılan) listesi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="8bd59-282">Açılır öğe içinde belirtilen **özellikleri** öğesini kullanarak bir **öğesi** öğesi.</span><span class="sxs-lookup"><span data-stu-id="8bd59-282">The dropdown items are specified within the **Properties** element using an **Item** element.</span></span> <span data-ttu-id="8bd59-283">**Kimliği** her **öğesi** benzersiz olmalıdır ve geçerli bir R değişken.</span><span class="sxs-lookup"><span data-stu-id="8bd59-283">The **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="8bd59-284">Değeri **adı** , bir **öğesi** gördüğünüz metin ve R işlevine geçirilen değer olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="8bd59-284">The value of the **name** of an **Item** serves as both the text that you see and the value that is passed to the R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="8bd59-285">*İsteğe bağlı özellikler*:</span><span class="sxs-lookup"><span data-stu-id="8bd59-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="8bd59-286">**Varsayılan** -varsayılan özelliği için değer birinden bir ID değeriyle eşleşmelidir **öğesi** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="8bd59-286">**default** - The value for the default property must correspond with an id value from one of the **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="8bd59-287">Yardımcı dosyalar</span><span class="sxs-lookup"><span data-stu-id="8bd59-287">Auxiliary Files</span></span>
<span data-ttu-id="8bd59-288">Özel Modül ZIP dosyasında yerleştirilen herhangi bir dosyayı yürütme sırasında kullanılabilir olacak.</span><span class="sxs-lookup"><span data-stu-id="8bd59-288">Any file that is placed in your custom module ZIP file is going to be available for use during execution time.</span></span> <span data-ttu-id="8bd59-289">Mevcut herhangi bir dizin yapıları korunur.</span><span class="sxs-lookup"><span data-stu-id="8bd59-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="8bd59-290">Bu works kaynak dosyayı aynı yerel olarak ve Azure Machine Learning yürütme anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8bd59-290">This means that file sourcing works the same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="8bd59-291">Tüm yola sahip olmanız gerekir böylece tüm dosyalar 'src' dizinine ayıklanır fark ' src /' öneki.</span><span class="sxs-lookup"><span data-stu-id="8bd59-291">Notice that all files are extracted to ‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="8bd59-292">Örneğin, NAs ile herhangi bir satır kümesinden kaldırmak ve herhangi bir yinelenen satır CustomAddRows çıktısı önce de kaldırmak istiyor ve bir dosyada RemoveDupNARows.R yapan bir R işlevi zaten yazdıktan söyleyin:</span><span class="sxs-lookup"><span data-stu-id="8bd59-292">For example, say you want to remove any rows with NAs from the dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="8bd59-293">CustomAddRows işlevi yardımcı dosyasında RemoveDupNARows.R kaynak:</span><span class="sxs-lookup"><span data-stu-id="8bd59-293">You can source the auxiliary file RemoveDupNARows.R in the CustomAddRows function:</span></span>

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

<span data-ttu-id="8bd59-294">Ardından, 'CustomAddRows.R', 'CustomAddRows.xml' ve 'RemoveDupNARows.R' özel bir R modülü olarak içeren bir zip dosyası karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8bd59-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="8bd59-295">Yürütme Ortamı</span><span class="sxs-lookup"><span data-stu-id="8bd59-295">Execution Environment</span></span>
<span data-ttu-id="8bd59-296">R betiği yürütme ortamı R aynı sürümünü kullandığından **R betiği yürütün** modülü ve aynı varsayılan paketleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd59-296">The execution environment for the R script uses the same version of R as the **Execute R Script** module and can use the same default packages.</span></span> <span data-ttu-id="8bd59-297">Özel Modül zip pakete dahil ederek özel modülünüzün ek R paketleri de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bd59-297">You can also add additional R packages to your custom module by including them in the custom module zip package.</span></span> <span data-ttu-id="8bd59-298">Yalnızca kendi R ortamında gibi bunları R komut dosyanıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8bd59-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="8bd59-299">**Yürütme Ortamı sınırlamaları** içerir:</span><span class="sxs-lookup"><span data-stu-id="8bd59-299">**Limitations of the execution environment** include:</span></span>

* <span data-ttu-id="8bd59-300">Kalıcı olmayan dosya sistemi: özel modülü çalıştırdığınızda yazılmış dosyaları aynı modülü birden çok çalıştırmaları arasında sürdürülmez.</span><span class="sxs-lookup"><span data-stu-id="8bd59-300">Non-persistent file system: Files written when the custom module is run are not persisted across multiple runs of the same module.</span></span>
* <span data-ttu-id="8bd59-301">Ağ erişim yok</span><span class="sxs-lookup"><span data-stu-id="8bd59-301">No network access</span></span>

