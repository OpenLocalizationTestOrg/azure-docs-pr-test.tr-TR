---
title: "Machine Learning Studio'ya veri içeri aktarma | Microsoft Docs"
description: "Azure Machine Learning Studio çeşitli veri kaynaklarından veri aktarmak nasıl. Hangi veri türleri ve veri biçimleri desteklenir öğrenin."
keywords: "veriler, veri biçimi, veri türleri, veri kaynakları, eğitim verilerini içeri aktarma"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: b92b480e62f4ce4f4836dc5d0f6afbe80c6b664a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="58afd-105">Eğitim verilerinizi çeşitli veri kaynaklarından Azure Machine Learning Studio’ya alma</span><span class="sxs-lookup"><span data-stu-id="58afd-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="58afd-106">Geliştirmek ve Tahmine dayalı analiz çözümü eğitmek için Machine Learning Studio'da kendi verilerinizi kullanmak için aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="58afd-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="58afd-107">Verileri yüklemek bir **yerel dosya** çalışma alanınızda bir veri kümesi modülü oluşturmak için sabit sürücünüzden vaktinden</span><span class="sxs-lookup"><span data-stu-id="58afd-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span></span>
* <span data-ttu-id="58afd-108">erişim verileri birinden birkaç **çevrimiçi veri kaynakları** denemenizi kullanarak çalışırken [veri içeri aktarma] [ import-data] Modülü</span><span class="sxs-lookup"><span data-stu-id="58afd-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span></span> 
* <span data-ttu-id="58afd-109">verileri başka bir Azure Machine learning kullanarak **denemeler** bir veri kümesi kaydedildi</span><span class="sxs-lookup"><span data-stu-id="58afd-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="58afd-110">Şirket içi verileri kullanan **SQL Server veritabanı**</span><span class="sxs-lookup"><span data-stu-id="58afd-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="58afd-111">Bu seçeneklerin her biri konulardan birine menüsünde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="58afd-111">Each of these options is described in one of the topics on the menu below.</span></span> <span data-ttu-id="58afd-112">Bu konular Machine Learning Studio'da kullanmak için bu çeşitli veri kaynaklarından veri içeri aktarma gösterir.</span><span class="sxs-lookup"><span data-stu-id="58afd-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="58afd-113">Eğitim verileri için kullanabileceğiniz bir Machine Learning Studio'da kullanılabilir birçok örnek veri kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="58afd-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="58afd-114">Bunlar hakkında daha fazla bilgi için bkz: [Azure Machine Learning Studio'daki örnek veri kümelerini kullanan](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="58afd-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="58afd-115">Bu giriş konu aynı zamanda veri Machine Learning Studio'da kullanım için hazır hale getirmek nasıl açıklanır ve hangi veri biçimleri ve veri türleri desteklenir açıklar.</span><span class="sxs-lookup"><span data-stu-id="58afd-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="58afd-116">Azure Machine Learning Studio'da kullanılmaya hazır veri al</span><span class="sxs-lookup"><span data-stu-id="58afd-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="58afd-117">Machine Learning Studio, ayrılmış veya bazı durumlarda dikdörtgen olmayan veri kullanılabilmesine rağmen bir veritabanındaki verileri yapılandırılmış metin verileri gibi dikdörtgen veya tablo verilerle çalışmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="58afd-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="58afd-118">Verilerinizi görece temiz ise en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="58afd-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="58afd-119">Diğer bir deyişle, tırnak işareti olmayan dizeler gibi sorunların denemenize verileri karşıya yüklemeden önce ilgilenebilmek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="58afd-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span></span>

<span data-ttu-id="58afd-120">Ancak, yok modülleri Machine Learning Studio'daki, bazı işleme denemenizi içindeki verilerin etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="58afd-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="58afd-121">Bağlı olarak makine öğrenimi algoritmaları kullanıyor olmanız, eksik değerleri ve seyrek veri gibi veri yapısal sorunların nasıl ele alacağız karar vermeniz gerekebilir ve ile yardımcı olabilecek modülleri vardır.</span><span class="sxs-lookup"><span data-stu-id="58afd-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="58afd-122">Bakılacak yer **veri dönüştürme** bu işlevleri gerçekleştirmek modülleri için modül paletinin bölümü.</span><span class="sxs-lookup"><span data-stu-id="58afd-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span></span>

<span data-ttu-id="58afd-123">Denemenizin herhangi bir noktada görüntüleyebilir veya çıkış bağlantı noktasına tıklayarak modülü tarafından üretilen veri indirin.</span><span class="sxs-lookup"><span data-stu-id="58afd-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span></span> <span data-ttu-id="58afd-124">Modül bağlı olarak farklı indirme seçenekleri kullanılabilir olabilir veya Machine Learning Studio'da web tarayıcınızdan görselleştirmek mümkün olabilir.</span><span class="sxs-lookup"><span data-stu-id="58afd-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="58afd-125">Desteklenen veri biçimleri ve veri türleri</span><span class="sxs-lookup"><span data-stu-id="58afd-125">Data formats and data types supported</span></span>
<span data-ttu-id="58afd-126">Veri türlerinin sayısı denemenize içeri aktarabilirsiniz, mekanizmaya bağlı olarak veri ve burada bu geldiği içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="58afd-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span></span>

* <span data-ttu-id="58afd-127">Düz metin (.txt)</span><span class="sxs-lookup"><span data-stu-id="58afd-127">Plain text (.txt)</span></span>
* <span data-ttu-id="58afd-128">Virgülle ayrılmış değerler (CSV bir başlık (.csv) ile veya olmadan) (. nh.csv)</span><span class="sxs-lookup"><span data-stu-id="58afd-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="58afd-129">Sekmeyle ayrılmış değerler (TSV bir başlık (.tsv) ile veya olmadan) (. nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="58afd-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="58afd-130">Excel dosyası</span><span class="sxs-lookup"><span data-stu-id="58afd-130">Excel file</span></span>
* <span data-ttu-id="58afd-131">Azure tablo</span><span class="sxs-lookup"><span data-stu-id="58afd-131">Azure table</span></span>
* <span data-ttu-id="58afd-132">Hive tablosu</span><span class="sxs-lookup"><span data-stu-id="58afd-132">Hive table</span></span>
* <span data-ttu-id="58afd-133">SQL veritabanı tablosu</span><span class="sxs-lookup"><span data-stu-id="58afd-133">SQL database table</span></span>
* <span data-ttu-id="58afd-134">OData değerleri</span><span class="sxs-lookup"><span data-stu-id="58afd-134">OData values</span></span>
* <span data-ttu-id="58afd-135">SVMLight veri (.svmlight) (bkz [SVMLight tanımı](http://svmlight.joachims.org/) biçimi bilgileri için)</span><span class="sxs-lookup"><span data-stu-id="58afd-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="58afd-136">Öznitelik ilişkisi dosya biçimi'ne (ARFF) veri (.arff) (bkz [ARFF tanımı](http://weka.wikispaces.com/ARFF) biçimi bilgileri için)</span><span class="sxs-lookup"><span data-stu-id="58afd-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="58afd-137">Zip dosyası (.zip)</span><span class="sxs-lookup"><span data-stu-id="58afd-137">Zip file (.zip)</span></span>
* <span data-ttu-id="58afd-138">R nesne ya da çalışma dosyası (. RData)</span><span class="sxs-lookup"><span data-stu-id="58afd-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="58afd-139">Meta verileri içeren ARFF gibi biçiminde veri içe aktarırsanız, Machine Learning Studio bu meta veriler başlık ve her sütunun veri türünü tanımlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="58afd-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span></span>

<span data-ttu-id="58afd-140">Bu meta verileri içermeyen TSV veya CSV biçiminde gibi verileri içe aktarırsanız, Machine Learning Studio verileri örnekleyerek her sütun için veri türü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="58afd-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span></span> <span data-ttu-id="58afd-141">Veri sütun başlıkları de yoksa, Machine Learning Studio varsayılan adlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="58afd-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="58afd-142">Açıkça belirtin veya kullanarak sütun başlıkları ve veri türlerini değiştirme [Düzenle meta veri][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="58afd-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="58afd-143">Aşağıdaki **veri türleri** Machine Learning Studio tarafından tanınan:</span><span class="sxs-lookup"><span data-stu-id="58afd-143">The following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="58afd-144">Dize</span><span class="sxs-lookup"><span data-stu-id="58afd-144">String</span></span>
* <span data-ttu-id="58afd-145">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="58afd-145">Integer</span></span>
* <span data-ttu-id="58afd-146">Çift</span><span class="sxs-lookup"><span data-stu-id="58afd-146">Double</span></span>
* <span data-ttu-id="58afd-147">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="58afd-147">Boolean</span></span>
* <span data-ttu-id="58afd-148">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="58afd-148">DateTime</span></span>
* <span data-ttu-id="58afd-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="58afd-149">TimeSpan</span></span>

<span data-ttu-id="58afd-150">Machine Learning Studio adlı bir iç veri türü kullanan ***veri tablosu*** modülleri arasında veri iletmek için.</span><span class="sxs-lookup"><span data-stu-id="58afd-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span></span> <span data-ttu-id="58afd-151">Veri tablosu biçimi kullanarak, verilerinizi açıkça dönüştürebilirsiniz [veri kümesine Dönüştür] [ convert-to-dataset] modülü.</span><span class="sxs-lookup"><span data-stu-id="58afd-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="58afd-152">Veri tablosu dışında biçimlerini kabul eden herhangi bir modül verileri veri tablosuna sessizce sonraki modülüne geçirmeden önce dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="58afd-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span></span>

<span data-ttu-id="58afd-153">Gerekirse, veri tablosu biçime geri CSV, TSV, ARFF veya diğer dönüştürme modülleri kullanarak SVMLight biçimine dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58afd-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="58afd-154">Bakılacak yer **veri formatı dönüştürme** bu işlevleri gerçekleştirmek modülleri için modül paletinin bölümü.</span><span class="sxs-lookup"><span data-stu-id="58afd-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
