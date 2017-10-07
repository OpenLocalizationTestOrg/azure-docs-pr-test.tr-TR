---
title: Machine Learning Studio aaaImport verisine | Microsoft Docs
description: "Nasıl tooimport Azure Machine Learning Studio çeşitli veri kaynaklarından verilerinizi. Hangi veri türleri ve veri biçimleri desteklenir öğrenin."
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
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="42cbb-105">Eğitim verilerinizi çeşitli veri kaynaklarından Azure Machine Learning Studio’ya alma</span><span class="sxs-lookup"><span data-stu-id="42cbb-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="42cbb-106">toouse kendi verilerinizi Machine Learning Studio toodevelop ve tren bir Tahmine dayalı analiz çözümü şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="42cbb-106">toouse your own data in Machine Learning Studio toodevelop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="42cbb-107">Verileri yüklemek bir **yerel dosya** ilerisinde çalışma alanınızda bir veri kümesi modülü, sabit sürücü toocreate saat</span><span class="sxs-lookup"><span data-stu-id="42cbb-107">upload data from a **local file** ahead of time from your hard drive toocreate a dataset module in your workspace</span></span>
* <span data-ttu-id="42cbb-108">erişim verileri birinden birkaç **çevrimiçi veri kaynakları** denemenizi hello kullanarak çalışırken [veri içeri aktarma] [ import-data] Modülü</span><span class="sxs-lookup"><span data-stu-id="42cbb-108">access data from one of several **online data sources** while your experiment is running using hello [Import Data][import-data] module</span></span> 
* <span data-ttu-id="42cbb-109">verileri başka bir Azure Machine learning kullanarak **denemeler** bir veri kümesi kaydedildi</span><span class="sxs-lookup"><span data-stu-id="42cbb-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="42cbb-110">Şirket içi verileri kullanan **SQL Server veritabanı**</span><span class="sxs-lookup"><span data-stu-id="42cbb-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="42cbb-111">Bu seçeneklerin her biri hello konulardan birine hello menüsünde aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="42cbb-111">Each of these options is described in one of hello topics on hello menu below.</span></span> <span data-ttu-id="42cbb-112">Bu konularda size nasıl toouse Machine Learning Studio'da tooimport verileri bu çeşitli veri kaynakları gösterir.</span><span class="sxs-lookup"><span data-stu-id="42cbb-112">These topics show you how tooimport data from these various data sources toouse in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="42cbb-113">Eğitim verileri için kullanabileceğiniz bir Machine Learning Studio'da kullanılabilir birçok örnek veri kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="42cbb-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="42cbb-114">Bunlar hakkında daha fazla bilgi için bkz: [hello örnek veri kümelerini Azure Machine Learning Studio'da kullanan](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="42cbb-114">For information on these, see [Use hello sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="42cbb-115">Bu giriş konu aynı zamanda tooget veri için hazır Machine Learning Studio'da kullanımını açıklar ve hangi veri biçimleri ve veri türleri desteklenir açıklar.</span><span class="sxs-lookup"><span data-stu-id="42cbb-115">This introductory topic also discusses how tooget data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="42cbb-116">Azure Machine Learning Studio'da kullanılmaya hazır veri al</span><span class="sxs-lookup"><span data-stu-id="42cbb-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="42cbb-117">Machine Learning Studio, ayrılmış veya bazı durumlarda dikdörtgen olmayan veri kullanılabilmesine rağmen bir veritabanındaki verileri yapılandırılmış metin verileri gibi dikdörtgen veya tablo verilerle tasarlanmış toowork ' dir.</span><span class="sxs-lookup"><span data-stu-id="42cbb-117">Machine Learning Studio is designed toowork with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="42cbb-118">Verilerinizi görece temiz ise en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="42cbb-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="42cbb-119">Diğer bir deyişle, denemenize hello verileri karşıya yüklemeden önce tootake tırnak işareti olmayan dizeler gibi sorunlar care of isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="42cbb-119">That is, you'll want tootake care of issues such as unquoted strings before you upload hello data into your experiment.</span></span>

<span data-ttu-id="42cbb-120">Ancak, yok modülleri Machine Learning Studio'daki, bazı işleme denemenizi içindeki verilerin etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="42cbb-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="42cbb-121">Kullanıyor hello machine learning algoritmaları bağlı olarak, toodecide nasıl gerekebilir eksik değerleri ve seyrek veri gibi veri yapısal sorunları ele alacağız ve ile yardımcı olabilecek modülleri vardır.</span><span class="sxs-lookup"><span data-stu-id="42cbb-121">Depending on hello machine learning algorithms you'll be using, you may need toodecide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="42cbb-122">Hello Ara **veri dönüştürme** hello modül paleti bu işlevleri gerçekleştirmek modüller bölümü.</span><span class="sxs-lookup"><span data-stu-id="42cbb-122">Look in hello **Data Transformation** section of hello module palette for modules that perform these functions.</span></span>

<span data-ttu-id="42cbb-123">Denemenizin herhangi bir noktada görüntüleyebilir veya hello çıkış bağlantı noktasına tıklayarak modülü tarafından üretilen hello veri indirin.</span><span class="sxs-lookup"><span data-stu-id="42cbb-123">At any point in your experiment you can view or download hello data that's produced by a module by clicking hello output port.</span></span> <span data-ttu-id="42cbb-124">Merhaba modülü bağlı olarak farklı indirme seçenekleri kullanılabilir olabilir veya Machine Learning Studio'da web tarayıcınızdan mümkün toovisualize hello veri olabilir.</span><span class="sxs-lookup"><span data-stu-id="42cbb-124">Depending on hello module, there may be different download options available, or you may be able toovisualize hello data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="42cbb-125">Desteklenen veri biçimleri ve veri türleri</span><span class="sxs-lookup"><span data-stu-id="42cbb-125">Data formats and data types supported</span></span>
<span data-ttu-id="42cbb-126">Veri türlerinin sayısı denemenize içeri aktarabilirsiniz, bağlı olarak hangi mekanizması tooimport veri ve burada bu geldiği kullanın:</span><span class="sxs-lookup"><span data-stu-id="42cbb-126">You can import a number of data types into your experiment, depending on what mechanism you use tooimport data and where it's coming from:</span></span>

* <span data-ttu-id="42cbb-127">Düz metin (.txt)</span><span class="sxs-lookup"><span data-stu-id="42cbb-127">Plain text (.txt)</span></span>
* <span data-ttu-id="42cbb-128">Virgülle ayrılmış değerler (CSV bir başlık (.csv) ile veya olmadan) (. nh.csv)</span><span class="sxs-lookup"><span data-stu-id="42cbb-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="42cbb-129">Sekmeyle ayrılmış değerler (TSV bir başlık (.tsv) ile veya olmadan) (. nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="42cbb-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="42cbb-130">Excel dosyası</span><span class="sxs-lookup"><span data-stu-id="42cbb-130">Excel file</span></span>
* <span data-ttu-id="42cbb-131">Azure tablo</span><span class="sxs-lookup"><span data-stu-id="42cbb-131">Azure table</span></span>
* <span data-ttu-id="42cbb-132">Hive tablosu</span><span class="sxs-lookup"><span data-stu-id="42cbb-132">Hive table</span></span>
* <span data-ttu-id="42cbb-133">SQL veritabanı tablosu</span><span class="sxs-lookup"><span data-stu-id="42cbb-133">SQL database table</span></span>
* <span data-ttu-id="42cbb-134">OData değerleri</span><span class="sxs-lookup"><span data-stu-id="42cbb-134">OData values</span></span>
* <span data-ttu-id="42cbb-135">SVMLight veri (.svmlight) (Merhaba bkz [SVMLight tanımı](http://svmlight.joachims.org/) biçimi bilgileri için)</span><span class="sxs-lookup"><span data-stu-id="42cbb-135">SVMLight data (.svmlight) (see hello [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="42cbb-136">Öznitelik ilişkisi dosya biçimi'ne (ARFF) veri (.arff) (Merhaba bkz [ARFF tanımı](http://weka.wikispaces.com/ARFF) biçimi bilgileri için)</span><span class="sxs-lookup"><span data-stu-id="42cbb-136">Attribute Relation File Format (ARFF) data (.arff) (see hello [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="42cbb-137">Zip dosyası (.zip)</span><span class="sxs-lookup"><span data-stu-id="42cbb-137">Zip file (.zip)</span></span>
* <span data-ttu-id="42cbb-138">R nesne ya da çalışma dosyası (. RData)</span><span class="sxs-lookup"><span data-stu-id="42cbb-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="42cbb-139">Meta verileri içeren ARFF gibi biçiminde veri içe aktarırsanız, Machine Learning Studio bu meta verileri toodefine hello başlığı ve her sütunun veri türünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="42cbb-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata toodefine hello heading and data type of each column.</span></span>

<span data-ttu-id="42cbb-140">Bu meta verileri içermeyen TSV veya CSV biçiminde gibi verileri içe aktarırsanız, Machine Learning Studio hello veri örnekleyerek her sütun için hello veri türü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="42cbb-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers hello data type for each column by sampling hello data.</span></span> <span data-ttu-id="42cbb-141">Merhaba veri sütun başlıkları de yoksa, Machine Learning Studio varsayılan adlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="42cbb-141">If hello data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="42cbb-142">Açıkça belirtin veya hello kullanarak sütunlar için hello başlıkları ve veri türlerini değiştirme [Düzenle meta veri][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="42cbb-142">You can explicitly specify or change hello headings and data types for columns using hello [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="42cbb-143">Merhaba aşağıdaki **veri türleri** Machine Learning Studio tarafından tanınan:</span><span class="sxs-lookup"><span data-stu-id="42cbb-143">hello following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="42cbb-144">Dize</span><span class="sxs-lookup"><span data-stu-id="42cbb-144">String</span></span>
* <span data-ttu-id="42cbb-145">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="42cbb-145">Integer</span></span>
* <span data-ttu-id="42cbb-146">Çift</span><span class="sxs-lookup"><span data-stu-id="42cbb-146">Double</span></span>
* <span data-ttu-id="42cbb-147">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="42cbb-147">Boolean</span></span>
* <span data-ttu-id="42cbb-148">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="42cbb-148">DateTime</span></span>
* <span data-ttu-id="42cbb-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="42cbb-149">TimeSpan</span></span>

<span data-ttu-id="42cbb-150">Machine Learning Studio adlı bir iç veri türü kullanan ***veri tablosu*** modülleri arasında toopass veri.</span><span class="sxs-lookup"><span data-stu-id="42cbb-150">Machine Learning Studio uses an internal data type called ***Data Table*** toopass data between modules.</span></span> <span data-ttu-id="42cbb-151">Verilerinizi açıkça hello kullanarak veri tablosu biçime dönüştürebilirsiniz [Dönüştür tooDataset] [ convert-to-dataset] modülü.</span><span class="sxs-lookup"><span data-stu-id="42cbb-151">You can explicitly convert your data into Data Table format using hello [Convert tooDataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="42cbb-152">Veri tablosu dışında biçimlerini kabul eden herhangi bir modül hello veri tooData tablo toohello sonraki modüle geçirmeden önce sessiz bir şekilde dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="42cbb-152">Any module that accepts formats other than Data Table will convert hello data tooData Table silently before passing it toohello next module.</span></span>

<span data-ttu-id="42cbb-153">Gerekirse, veri tablosu biçime geri CSV, TSV, ARFF veya diğer dönüştürme modülleri kullanarak SVMLight biçimine dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42cbb-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="42cbb-154">Hello Ara **veri formatı dönüştürme** hello modül paleti bu işlevleri gerçekleştirmek modüller bölümü.</span><span class="sxs-lookup"><span data-stu-id="42cbb-154">Look in hello **Data Format Conversions** section of hello module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
