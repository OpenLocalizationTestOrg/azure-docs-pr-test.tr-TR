---
title: "Azure Data Factory aaaFile ve sıkıştırma biçimlerde | Microsoft Docs"
description: "Azure Data Factory ile desteklenen hello dosya biçimleri hakkında bilgi edinin."
keywords: BLOB verilerini, azure blob kopyalama
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="2a13d-104">Azure Data Factory tarafından desteklenen dosya ve sıkıştırma biçimleri</span><span class="sxs-lookup"><span data-stu-id="2a13d-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="2a13d-105">*Bu konu, bağlayıcıları aşağıdaki toohello geçerlidir: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [dosya sistemi](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), ve [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="2a13d-105">*This topic applies toohello following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="2a13d-106">Azure Data Factory hello şu dosya biçimi türlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="2a13d-106">Azure Data Factory supports hello following file format types:</span></span>

* [<span data-ttu-id="2a13d-107">Metin biçimi</span><span class="sxs-lookup"><span data-stu-id="2a13d-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="2a13d-108">JSON biçimi</span><span class="sxs-lookup"><span data-stu-id="2a13d-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="2a13d-109">Avro biçimi</span><span class="sxs-lookup"><span data-stu-id="2a13d-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="2a13d-110">ORC biçimi</span><span class="sxs-lookup"><span data-stu-id="2a13d-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="2a13d-111">Parquet biçimi</span><span class="sxs-lookup"><span data-stu-id="2a13d-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="2a13d-112">Metin biçimi</span><span class="sxs-lookup"><span data-stu-id="2a13d-112">Text format</span></span>
<span data-ttu-id="2a13d-113">Bir metin dosyasından tooread istediğiniz veya tooa metin dosyasına yazma, hello ayarlayın `type` hello özelliğinde `format` hello dataset bölümü çok**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-113">If you want tooread from a text file or write tooa text file, set hello `type` property in hello `format` section of hello dataset too**TextFormat**.</span></span> <span data-ttu-id="2a13d-114">Merhaba aşağıdakileri de belirtebilirsiniz **isteğe bağlı** hello özelliklerinde `format` bölümü.</span><span class="sxs-lookup"><span data-stu-id="2a13d-114">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="2a13d-115">Bkz: [TextFormat örnek](#textformat-example) nasıl bölüm tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="2a13d-115">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="2a13d-116">Özellik</span><span class="sxs-lookup"><span data-stu-id="2a13d-116">Property</span></span> | <span data-ttu-id="2a13d-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2a13d-117">Description</span></span> | <span data-ttu-id="2a13d-118">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="2a13d-118">Allowed values</span></span> | <span data-ttu-id="2a13d-119">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2a13d-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2a13d-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="2a13d-120">columnDelimiter</span></span> |<span data-ttu-id="2a13d-121">Merhaba karakter tooseparate sütunları bir dosyada kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a13d-121">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="2a13d-122">Verilerinizi değil olasılıkla olabilir nadir bir yazdırılamayan karakter var. toouse düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a13d-122">You can consider toouse a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="2a13d-123">Örneğin, Başlat, başlık (SOH) temsil eder "\u0001" belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a13d-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="2a13d-124">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-124">Only one character is allowed.</span></span> <span data-ttu-id="2a13d-125">Merhaba **varsayılan** değer **virgül (',')**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-125">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="2a13d-126">toouse bir Unicode karakter başvurmak çok[Unicode karakterler](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello ilgili kod için.</span><span class="sxs-lookup"><span data-stu-id="2a13d-126">toouse a Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="2a13d-127">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-127">No</span></span> |
| <span data-ttu-id="2a13d-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="2a13d-128">rowDelimiter</span></span> |<span data-ttu-id="2a13d-129">Merhaba karakter tooseparate satır bir dosyada kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a13d-129">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="2a13d-130">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-130">Only one character is allowed.</span></span> <span data-ttu-id="2a13d-131">Merhaba **varsayılan** değerdir herhangi biri üzerinde okuma değerleri aşağıdaki hello: **["\r\n", "\r", "\n"]** ve **"\r\n"** yazma üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2a13d-131">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="2a13d-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-132">No</span></span> |
| <span data-ttu-id="2a13d-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="2a13d-133">escapeChar</span></span> |<span data-ttu-id="2a13d-134">Merhaba özel karakter tooescape bir sütun ayırıcısı giriş dosyası hello içeriğinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a13d-134">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="2a13d-135">Bir tablo için hem escapeChar hem de quoteChar parametrelerini aynı anda belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a13d-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="2a13d-136">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-136">Only one character is allowed.</span></span> <span data-ttu-id="2a13d-137">Varsayılan değer yoktur.</span><span class="sxs-lookup"><span data-stu-id="2a13d-137">No default value.</span></span> <br/><br/><span data-ttu-id="2a13d-138">Örnek: virgül varsa (', ') hello sütun sınırlayıcı ancak toohave hello virgül karakteri hello metin istediğiniz şekilde (örnek: "Hello, world"), '$' hello kaçış karakteri olarak tanımlamak ve dizesi kullanın "$Hello, world" Merhaba kaynağındaki.</span><span class="sxs-lookup"><span data-stu-id="2a13d-138">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="2a13d-139">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-139">No</span></span> |
| <span data-ttu-id="2a13d-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="2a13d-140">quoteChar</span></span> |<span data-ttu-id="2a13d-141">Merhaba karakter tooquote bir dize değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a13d-141">hello character used tooquote a string value.</span></span> <span data-ttu-id="2a13d-142">Hello sütun ve satır sınırlayıcıları hello tırnak karakterleri içine hello dize değeri bir parçası olarak değerlendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="2a13d-142">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="2a13d-143">Bu özellik geçerli tooboth girdidir ve çıkış veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="2a13d-143">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="2a13d-144">Bir tablo için hem escapeChar hem de quoteChar parametrelerini aynı anda belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a13d-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="2a13d-145">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-145">Only one character is allowed.</span></span> <span data-ttu-id="2a13d-146">Varsayılan değer yoktur.</span><span class="sxs-lookup"><span data-stu-id="2a13d-146">No default value.</span></span> <br/><br/><span data-ttu-id="2a13d-147">Virgül varsa, örneğin, (', ') hello sütun sınırlayıcı ancak toohave virgül karakteri hello metin istediğiniz gibi (örnek: < Hello, world >), tanımlayabileceğiniz "(tırnak) tırnak işareti karakteri hello ve hello dizesini kullanın"Hello, world"Merhaba kaynağındaki.</span><span class="sxs-lookup"><span data-stu-id="2a13d-147">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="2a13d-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-148">No</span></span> |
| <span data-ttu-id="2a13d-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="2a13d-149">nullValue</span></span> |<span data-ttu-id="2a13d-150">Bir veya daha fazla karakter toorepresent bir null değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a13d-150">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="2a13d-151">Bir veya daha fazla karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-151">One or more characters.</span></span> <span data-ttu-id="2a13d-152">Merhaba **varsayılan** değerler **"\N" ve "NULL"** okunur ve **"\N"** yazma üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2a13d-152">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="2a13d-153">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-153">No</span></span> |
| <span data-ttu-id="2a13d-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="2a13d-154">encodingName</span></span> |<span data-ttu-id="2a13d-155">Merhaba kodlama adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a13d-155">Specify hello encoding name.</span></span> |<span data-ttu-id="2a13d-156">Geçerli bir kodlama adı.</span><span class="sxs-lookup"><span data-stu-id="2a13d-156">A valid encoding name.</span></span> <span data-ttu-id="2a13d-157">Bkz. [Encoding.EncodingName Özelliği](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a13d-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="2a13d-158">Örnek: windows-1250 veya shift_jis.</span><span class="sxs-lookup"><span data-stu-id="2a13d-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="2a13d-159">Merhaba **varsayılan** değer **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-159">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="2a13d-160">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-160">No</span></span> |
| <span data-ttu-id="2a13d-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="2a13d-161">firstRowAsHeader</span></span> |<span data-ttu-id="2a13d-162">Tooconsider ilk satır bir başlık olarak hello olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-162">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="2a13d-163">Giriş veri kümesinde Data Factory ilk satırı üst bilgi olarak okur.</span><span class="sxs-lookup"><span data-stu-id="2a13d-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="2a13d-164">Çıkış veri kümesinde Data Factory ilk satırı üst bilgi olarak yazar.</span><span class="sxs-lookup"><span data-stu-id="2a13d-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="2a13d-165">Örnek senaryolar için bkz. [`firstRowAsHeader` ve `skipLineCount` kullanım senaryoları](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="2a13d-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="2a13d-166">True</span><span class="sxs-lookup"><span data-stu-id="2a13d-166">True</span></span><br/><span data-ttu-id="2a13d-167"><b>False (varsayılan)</b></span><span class="sxs-lookup"><span data-stu-id="2a13d-167"><b>False (default)</b></span></span> |<span data-ttu-id="2a13d-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-168">No</span></span> |
| <span data-ttu-id="2a13d-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="2a13d-169">skipLineCount</span></span> |<span data-ttu-id="2a13d-170">Giriş dosyaları veri okuma satırları tooskip Hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-170">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="2a13d-171">SkipLineCount ve firstRowAsHeader belirtilirse, hello satırlar ilk atlanır ve hello üst bilgileri hello giriş dosyasından sonra okuyun.</span><span class="sxs-lookup"><span data-stu-id="2a13d-171">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="2a13d-172">Örnek senaryolar için bkz. [`firstRowAsHeader` ve `skipLineCount` kullanım senaryoları](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="2a13d-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="2a13d-173">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="2a13d-173">Integer</span></span> |<span data-ttu-id="2a13d-174">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-174">No</span></span> |
| <span data-ttu-id="2a13d-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="2a13d-175">treatEmptyAsNull</span></span> |<span data-ttu-id="2a13d-176">Bir null olarak tootreat null veya boş dize değeri olup olmadığını belirten bir giriş dosyasından veri okuma.</span><span class="sxs-lookup"><span data-stu-id="2a13d-176">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="2a13d-177">**True (varsayılan)**</span><span class="sxs-lookup"><span data-stu-id="2a13d-177">**True (default)**</span></span><br/><span data-ttu-id="2a13d-178">False</span><span class="sxs-lookup"><span data-stu-id="2a13d-178">False</span></span> |<span data-ttu-id="2a13d-179">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="2a13d-180">TextFormat örneği</span><span class="sxs-lookup"><span data-stu-id="2a13d-180">TextFormat example</span></span>
<span data-ttu-id="2a13d-181">Bir veri kümesi için JSON tanımını izleyen hello hello isteğe bağlı özelliklerin bazıları belirtilir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-181">In hello following JSON definition for a dataset, some of hello optional properties are specified.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="2a13d-182">toouse bir `escapeChar` yerine `quoteChar`, hello satırla değiştirin `quoteChar` escapeChar aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="2a13d-182">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="2a13d-183">firstRowAsHeader ve skipLineCount kullanım senaryoları</span><span class="sxs-lookup"><span data-stu-id="2a13d-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="2a13d-184">Dosya olmayan kaynak tooa metin dosyasından kopyalama ve tooadd hello şema meta verileri içeren bir başlık satırı istiyor musunuz (örneğin: SQL Şeması).</span><span class="sxs-lookup"><span data-stu-id="2a13d-184">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="2a13d-185">Belirtin `firstRowAsHeader` hello çıkış DataSet Bu senaryo için true.</span><span class="sxs-lookup"><span data-stu-id="2a13d-185">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="2a13d-186">Bir üst bilgi satırı tooa dosya olmayan havuz içeren bir metin dosyasından kopyalama ve satır toodrop istersiniz.</span><span class="sxs-lookup"><span data-stu-id="2a13d-186">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="2a13d-187">Belirtin `firstRowAsHeader` hello girdi veri kümesi olarak true.</span><span class="sxs-lookup"><span data-stu-id="2a13d-187">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="2a13d-188">Bir metin dosyasından kopyalama ve hiçbir veri veya üstbilgi bilgileri içeren birkaç satır hello başında tooskip istiyor.</span><span class="sxs-lookup"><span data-stu-id="2a13d-188">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="2a13d-189">Belirtin `skipLineCount` tooindicate hello satırları toobe sayısı atlandı.</span><span class="sxs-lookup"><span data-stu-id="2a13d-189">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="2a13d-190">Merhaba rest hello dosyasının bir başlık satırı içeriyorsa, ayrıca belirtebilirsiniz `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="2a13d-190">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="2a13d-191">Her iki `skipLineCount` ve `firstRowAsHeader` belirtilirse, hello satırları ilk atlanır ve hello üstbilgi bilgileri hello giriş dosyasından sonra okuyun</span><span class="sxs-lookup"><span data-stu-id="2a13d-191">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

## <a name="json-format"></a><span data-ttu-id="2a13d-192">JSON biçimi</span><span class="sxs-lookup"><span data-stu-id="2a13d-192">JSON format</span></span>
<span data-ttu-id="2a13d-193">çok**bir JSON dosyası olarak içeri/dışarı aktarma-olduğu içine/Azure Cosmos DB'den**, hello bakın [içeri/dışarı aktarma JSON belgeleri](data-factory-azure-documentdb-connector.md#importexport-json-documents) bölümüne [/Azure Cosmos DB'den veri taşıma](data-factory-azure-documentdb-connector.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="2a13d-193">too**import/export a JSON file as-is into/from Azure Cosmos DB**, hello see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="2a13d-194">Merhaba, tooparse hello JSON dosyaları veya JSON biçiminde hello veri yazmak istiyorsanız ayarlayın `type` hello özelliğinde `format` çok bölümünde**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-194">If you want tooparse hello JSON files or write hello data in JSON format, set hello `type` property in hello `format` section too**JsonFormat**.</span></span> <span data-ttu-id="2a13d-195">Merhaba aşağıdakileri de belirtebilirsiniz **isteğe bağlı** hello özelliklerinde `format` bölümü.</span><span class="sxs-lookup"><span data-stu-id="2a13d-195">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="2a13d-196">Bkz: [JsonFormat örnek](#jsonformat-example) nasıl bölüm tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="2a13d-196">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="2a13d-197">Özellik</span><span class="sxs-lookup"><span data-stu-id="2a13d-197">Property</span></span> | <span data-ttu-id="2a13d-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2a13d-198">Description</span></span> | <span data-ttu-id="2a13d-199">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2a13d-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a13d-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="2a13d-200">filePattern</span></span> |<span data-ttu-id="2a13d-201">Her JSON dosyasında depolanan verilerin Hello desen belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a13d-201">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="2a13d-202">İzin verilen değerler: **setOfObjects** ve **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="2a13d-203">Merhaba **varsayılan** değer **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-203">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="2a13d-204">Bu desenler hakkında ayrıntılı bilgi için bkz. [JSON dosyası desenleri](#json-file-patterns).</span><span class="sxs-lookup"><span data-stu-id="2a13d-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="2a13d-205">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-205">No</span></span> |
| <span data-ttu-id="2a13d-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="2a13d-206">jsonNodeReference</span></span> | <span data-ttu-id="2a13d-207">Bir dizinin içindeki hello nesnelerinden verileri ayıklamak ve tooiterate isterseniz hello ile aynı alan desen, bu dizinin hello JSON yolu belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a13d-207">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="2a13d-208">Bu özellik yalnızca JSON dosyalarından veri kopyalarken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="2a13d-209">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-209">No</span></span> |
| <span data-ttu-id="2a13d-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="2a13d-210">jsonPathDefinition</span></span> | <span data-ttu-id="2a13d-211">Merhaba JSON yol ifadesi her sütun eşlemesi için özelleştirilmiş sütun adıyla (küçük başlayın) belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a13d-211">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="2a13d-212">Bu özellik yalnızca JSON dosyalarından veri kopyalarken desteklenir. Verileri nesne veya diziden ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a13d-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="2a13d-213">Kök nesnede altında alanlar için kök $ ile Başlat; tarafından seçilen hello dizinin içindeki alanlar için `jsonNodeReference` özelliği, hello dizi öğesinin başından.</span><span class="sxs-lookup"><span data-stu-id="2a13d-213">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="2a13d-214">Bkz: [JsonFormat örnek](#jsonformat-example) nasıl bölüm tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="2a13d-214">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="2a13d-215">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-215">No</span></span> |
| <span data-ttu-id="2a13d-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="2a13d-216">encodingName</span></span> |<span data-ttu-id="2a13d-217">Merhaba kodlama adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a13d-217">Specify hello encoding name.</span></span> <span data-ttu-id="2a13d-218">Geçerli kodlama adlar Hello listesi için bkz: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) özelliği.</span><span class="sxs-lookup"><span data-stu-id="2a13d-218">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="2a13d-219">Örneğin: windows-1250 veya shift_jis.</span><span class="sxs-lookup"><span data-stu-id="2a13d-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="2a13d-220">Merhaba **varsayılan** değer: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-220">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="2a13d-221">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-221">No</span></span> |
| <span data-ttu-id="2a13d-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="2a13d-222">nestingSeparator</span></span> |<span data-ttu-id="2a13d-223">Kullanılan tooseparate iç içe geçme düzeyi karakter.</span><span class="sxs-lookup"><span data-stu-id="2a13d-223">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="2a13d-224">Merhaba varsayılan değer '.' (nokta).</span><span class="sxs-lookup"><span data-stu-id="2a13d-224">hello default value is '.' (dot).</span></span> |<span data-ttu-id="2a13d-225">Hayır</span><span class="sxs-lookup"><span data-stu-id="2a13d-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="2a13d-226">JSON dosyası desenleri</span><span class="sxs-lookup"><span data-stu-id="2a13d-226">JSON file patterns</span></span>

<span data-ttu-id="2a13d-227">Kopyalama etkinliği, JSON dosyalarınızın desenler izleyen hello ayrıştırma yapabilir:</span><span class="sxs-lookup"><span data-stu-id="2a13d-227">Copy activity can parse hello following patterns of JSON files:</span></span>

- <span data-ttu-id="2a13d-228">**1. Tür: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="2a13d-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="2a13d-229">Her dosya tek bir nesne veya satırlara ayrılmış/bitiştirilmiş birden fazla nesne içerir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="2a13d-230">Bu seçenek bir çıkış veri kümesinde belirlendiğinde, kopyalama etkinliği her satırda bir nesnenin bulunduğu (satırlara ayrılmış) tek bir JSON dosyası üretir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="2a13d-231">**tek nesne JSON örneği**</span><span class="sxs-lookup"><span data-stu-id="2a13d-231">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="2a13d-232">**satırlara ayrılmış JSON örneği**</span><span class="sxs-lookup"><span data-stu-id="2a13d-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="2a13d-233">**bitiştirilmiş JSON örneği**</span><span class="sxs-lookup"><span data-stu-id="2a13d-233">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="2a13d-234">**2. Tür: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="2a13d-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="2a13d-235">Her dosya bir nesne dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-235">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a><span data-ttu-id="2a13d-236">JsonFormat örneği</span><span class="sxs-lookup"><span data-stu-id="2a13d-236">JsonFormat example</span></span>

<span data-ttu-id="2a13d-237">**Örnek Durum 1: JSON dosyalarından veri kopyalama**</span><span class="sxs-lookup"><span data-stu-id="2a13d-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="2a13d-238">İki örnek verileri JSON dosyaları kopyalarken aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="2a13d-238">See hello following two samples when copying data from JSON files.</span></span> <span data-ttu-id="2a13d-239">Merhaba genel toonote noktaları:</span><span class="sxs-lookup"><span data-stu-id="2a13d-239">hello generic points toonote:</span></span>

<span data-ttu-id="2a13d-240">**Örnek 1: nesne ve diziden veri ayıklama**</span><span class="sxs-lookup"><span data-stu-id="2a13d-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="2a13d-241">Bu örnekte, bir kök JSON nesnesi toosingle kaydı tablo sonuç eşler bekler.</span><span class="sxs-lookup"><span data-stu-id="2a13d-241">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="2a13d-242">İçeriği aşağıdaki hello ile bir JSON dosyası varsa:</span><span class="sxs-lookup"><span data-stu-id="2a13d-242">If you have a JSON file with hello following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
<span data-ttu-id="2a13d-243">ve bunu bir Azure SQL tablosuna hello aşağıdaki biçimi, veri nesneleri hem dizi çıkartarak toocopy istiyor:</span><span class="sxs-lookup"><span data-stu-id="2a13d-243">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="2a13d-244">id</span><span class="sxs-lookup"><span data-stu-id="2a13d-244">id</span></span> | <span data-ttu-id="2a13d-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="2a13d-245">deviceType</span></span> | <span data-ttu-id="2a13d-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="2a13d-246">targetResourceType</span></span> | <span data-ttu-id="2a13d-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="2a13d-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="2a13d-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="2a13d-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="2a13d-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="2a13d-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="2a13d-250">PC</span><span class="sxs-lookup"><span data-stu-id="2a13d-250">PC</span></span> | <span data-ttu-id="2a13d-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="2a13d-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="2a13d-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="2a13d-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="2a13d-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="2a13d-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="2a13d-254">Merhaba girdi veri kümesi ile **JsonFormat** türü şu şekilde tanımlanır: (yalnızca hello ilgili bölümleri kısmi tanımıyla).</span><span class="sxs-lookup"><span data-stu-id="2a13d-254">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="2a13d-255">Daha ayrıntılı belirtmek gerekirse:</span><span class="sxs-lookup"><span data-stu-id="2a13d-255">More specifically:</span></span>

- <span data-ttu-id="2a13d-256">`structure`Bölüm tootabular veri dönüştürülürken özelleştirilmiş hello sütun adları ve hello karşılık gelen veri türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2a13d-256">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="2a13d-257">Bu bölüm **isteğe bağlı** toodo sütun eşlemesi gerekmedikçe.</span><span class="sxs-lookup"><span data-stu-id="2a13d-257">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="2a13d-258">Bkz: [kaynak veri kümesi sütunları toodestination dataset sütunlara](data-factory-map-columns.md) daha fazla ayrıntı için bölüm.</span><span class="sxs-lookup"><span data-stu-id="2a13d-258">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="2a13d-259">`jsonPathDefinition`Burada tooextract hello verilerden belirten her sütun için Hello JSON yolu belirtir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-259">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="2a13d-260">kullanabileceğiniz toocopy veri dizisinden **array [x] .property** özelliği hello un x. nesne veya size verilen hello tooextract değerini kullanabilir  **dizisi [*] .property** toofind Böyle bir özellik içeren herhangi bir nesneden Hello değeri.</span><span class="sxs-lookup"><span data-stu-id="2a13d-260">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

<span data-ttu-id="2a13d-261">**Örnek 2: çapraz hello aynı diziden desen ile birden çok nesne uygulayın.**</span><span class="sxs-lookup"><span data-stu-id="2a13d-261">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="2a13d-262">Bu örnekte, tablo sonuç içinde birden çok kayıt içine tootransform bir kök JSON nesnesi bekler.</span><span class="sxs-lookup"><span data-stu-id="2a13d-262">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="2a13d-263">İçeriği aşağıdaki hello ile bir JSON dosyası varsa:</span><span class="sxs-lookup"><span data-stu-id="2a13d-263">If you have a JSON file with hello following content:</span></span>  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
<span data-ttu-id="2a13d-264">ve bunu bir Azure SQL tablosuna hello aşağıdaki biçiminde hello veri hello dizinin içindeki düzleştirme tarafından toocopy istediğiniz ve çapraz birleştirme hello ortak kök bilgileri ile:</span><span class="sxs-lookup"><span data-stu-id="2a13d-264">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="2a13d-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="2a13d-265">ordernumber</span></span> | <span data-ttu-id="2a13d-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="2a13d-266">orderdate</span></span> | <span data-ttu-id="2a13d-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="2a13d-267">order_pd</span></span> | <span data-ttu-id="2a13d-268">order_price</span><span class="sxs-lookup"><span data-stu-id="2a13d-268">order_price</span></span> | <span data-ttu-id="2a13d-269">city</span><span class="sxs-lookup"><span data-stu-id="2a13d-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="2a13d-270">01</span><span class="sxs-lookup"><span data-stu-id="2a13d-270">01</span></span> | <span data-ttu-id="2a13d-271">20170122</span><span class="sxs-lookup"><span data-stu-id="2a13d-271">20170122</span></span> | <span data-ttu-id="2a13d-272">P1</span><span class="sxs-lookup"><span data-stu-id="2a13d-272">P1</span></span> | <span data-ttu-id="2a13d-273">23</span><span class="sxs-lookup"><span data-stu-id="2a13d-273">23</span></span> | <span data-ttu-id="2a13d-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="2a13d-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="2a13d-275">01</span><span class="sxs-lookup"><span data-stu-id="2a13d-275">01</span></span> | <span data-ttu-id="2a13d-276">20170122</span><span class="sxs-lookup"><span data-stu-id="2a13d-276">20170122</span></span> | <span data-ttu-id="2a13d-277">P2</span><span class="sxs-lookup"><span data-stu-id="2a13d-277">P2</span></span> | <span data-ttu-id="2a13d-278">13</span><span class="sxs-lookup"><span data-stu-id="2a13d-278">13</span></span> | <span data-ttu-id="2a13d-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="2a13d-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="2a13d-280">01</span><span class="sxs-lookup"><span data-stu-id="2a13d-280">01</span></span> | <span data-ttu-id="2a13d-281">20170122</span><span class="sxs-lookup"><span data-stu-id="2a13d-281">20170122</span></span> | <span data-ttu-id="2a13d-282">P3</span><span class="sxs-lookup"><span data-stu-id="2a13d-282">P3</span></span> | <span data-ttu-id="2a13d-283">231</span><span class="sxs-lookup"><span data-stu-id="2a13d-283">231</span></span> | <span data-ttu-id="2a13d-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="2a13d-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="2a13d-285">Merhaba girdi veri kümesi ile **JsonFormat** türü şu şekilde tanımlanır: (yalnızca hello ilgili bölümleri kısmi tanımıyla).</span><span class="sxs-lookup"><span data-stu-id="2a13d-285">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="2a13d-286">Daha ayrıntılı belirtmek gerekirse:</span><span class="sxs-lookup"><span data-stu-id="2a13d-286">More specifically:</span></span>

- <span data-ttu-id="2a13d-287">`structure`Bölüm tootabular veri dönüştürülürken özelleştirilmiş hello sütun adları ve hello karşılık gelen veri türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2a13d-287">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="2a13d-288">Bu bölüm **isteğe bağlı** toodo sütun eşlemesi gerekmedikçe.</span><span class="sxs-lookup"><span data-stu-id="2a13d-288">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="2a13d-289">Bkz: [kaynak veri kümesi sütunları toodestination dataset sütunlara](data-factory-map-columns.md) daha fazla ayrıntı için bölüm.</span><span class="sxs-lookup"><span data-stu-id="2a13d-289">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="2a13d-290">`jsonNodeReference`aynı desen altında hello hello nesneleriyle tooiterate ve ayıklama verilerini gösteren **dizi** orderlines.</span><span class="sxs-lookup"><span data-stu-id="2a13d-290">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="2a13d-291">`jsonPathDefinition`Burada tooextract hello verilerden belirten her sütun için Hello JSON yolu belirtir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-291">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="2a13d-292">Bu örnekte "$.", "order_pd" ve "order_price" "$" olmadan hello array öğesinden türetilen yoluyla tanımlı başlangıç JSON yolu ile kök nesnesi altında "ordernumber", "orderdate" ve "Şehir" olur.</span><span class="sxs-lookup"><span data-stu-id="2a13d-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

<span data-ttu-id="2a13d-293">**Hello aşağıdaki noktaları göz önünde bulundurun:**</span><span class="sxs-lookup"><span data-stu-id="2a13d-293">**Note hello following points:**</span></span>

* <span data-ttu-id="2a13d-294">Merhaba, `structure` ve `jsonPathDefinition` hello Data Factory veri kümesi içinde hello tanımlanmayan kopyalama etkinliği hello hello ilk nesne şemadan ve nesnenin tamamı hello düzleştirmek algılar.</span><span class="sxs-lookup"><span data-stu-id="2a13d-294">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="2a13d-295">Merhaba JSON girişi bir dizi varsa, varsayılan olarak hello kopyalama etkinliği hello tüm dizi değeri bir dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="2a13d-295">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="2a13d-296">Tooextract verileri kullanarak ondan seçebilirsiniz `jsonNodeReference` ve/veya `jsonPathDefinition`, veya içinde belirterek değil atlayabilirsiniz `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="2a13d-296">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="2a13d-297">Varsa yinelenen adları, aynı düzeydeki Merhaba, hello kopyalama etkinliği hello sonuncu seçer.</span><span class="sxs-lookup"><span data-stu-id="2a13d-297">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="2a13d-298">Özellik adları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="2a13d-298">Property names are case-sensitive.</span></span> <span data-ttu-id="2a13d-299">Aynı ada ancak farklı büyük/küçük harf düzenine sahip iki özellik, iki ayrı özellik olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="2a13d-300">**Durum 2: veri tooJSON dosyası yazılıyor**</span><span class="sxs-lookup"><span data-stu-id="2a13d-300">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="2a13d-301">SQL veritabanı tablosunda aşağıdaki hello varsa:</span><span class="sxs-lookup"><span data-stu-id="2a13d-301">If you have hello following table in SQL Database:</span></span>

| <span data-ttu-id="2a13d-302">id</span><span class="sxs-lookup"><span data-stu-id="2a13d-302">id</span></span> | <span data-ttu-id="2a13d-303">order_date</span><span class="sxs-lookup"><span data-stu-id="2a13d-303">order_date</span></span> | <span data-ttu-id="2a13d-304">order_price</span><span class="sxs-lookup"><span data-stu-id="2a13d-304">order_price</span></span> | <span data-ttu-id="2a13d-305">order_by</span><span class="sxs-lookup"><span data-stu-id="2a13d-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2a13d-306">1</span><span class="sxs-lookup"><span data-stu-id="2a13d-306">1</span></span> | <span data-ttu-id="2a13d-307">20170119</span><span class="sxs-lookup"><span data-stu-id="2a13d-307">20170119</span></span> | <span data-ttu-id="2a13d-308">2000</span><span class="sxs-lookup"><span data-stu-id="2a13d-308">2000</span></span> | <span data-ttu-id="2a13d-309">David</span><span class="sxs-lookup"><span data-stu-id="2a13d-309">David</span></span> |
| <span data-ttu-id="2a13d-310">2</span><span class="sxs-lookup"><span data-stu-id="2a13d-310">2</span></span> | <span data-ttu-id="2a13d-311">20170120</span><span class="sxs-lookup"><span data-stu-id="2a13d-311">20170120</span></span> | <span data-ttu-id="2a13d-312">3500</span><span class="sxs-lookup"><span data-stu-id="2a13d-312">3500</span></span> | <span data-ttu-id="2a13d-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="2a13d-313">Patrick</span></span> |
| <span data-ttu-id="2a13d-314">3</span><span class="sxs-lookup"><span data-stu-id="2a13d-314">3</span></span> | <span data-ttu-id="2a13d-315">20170121</span><span class="sxs-lookup"><span data-stu-id="2a13d-315">20170121</span></span> | <span data-ttu-id="2a13d-316">4000</span><span class="sxs-lookup"><span data-stu-id="2a13d-316">4000</span></span> | <span data-ttu-id="2a13d-317">Jason</span><span class="sxs-lookup"><span data-stu-id="2a13d-317">Jason</span></span> |

<span data-ttu-id="2a13d-318">ve her bir kaydı toowrite tooa JSON nesnesi biçimini izleyen hello beklediğiniz:</span><span class="sxs-lookup"><span data-stu-id="2a13d-318">and for each record, you expect toowrite tooa JSON object in hello following format:</span></span>
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="2a13d-319">Merhaba çıkış veri kümesi ile **JsonFormat** türü şu şekilde tanımlanır: (yalnızca hello ilgili bölümleri kısmi tanımıyla).</span><span class="sxs-lookup"><span data-stu-id="2a13d-319">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="2a13d-320">Daha belirgin olarak `structure` bölüm hedef dosyasında özelleştirilmiş hello özellik adlarını tanımlar `nestingSeparator` (varsayılan değer ".") hello adından kullanılan tooidentify hello iç içe katmandır.</span><span class="sxs-lookup"><span data-stu-id="2a13d-320">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") are used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="2a13d-321">Bu bölüm **isteğe bağlı** toochange hello özellik adı kaynak sütun adı ile karşılaştırmak istediğiniz ya da hello özelliklerden bazıları iç içe sürece.</span><span class="sxs-lookup"><span data-stu-id="2a13d-321">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a><span data-ttu-id="2a13d-322">AVRO biçimi</span><span class="sxs-lookup"><span data-stu-id="2a13d-322">AVRO format</span></span>
<span data-ttu-id="2a13d-323">Tooparse hello Avro dosyalarının istediğiniz veya Avro biçiminde hello veri yazmak istiyorsanız, hello ayarlayın `format` `type` özelliği çok**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-323">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="2a13d-324">Merhaba typeProperties bölüm içindeki hello biçimi bölümünde herhangi bir özellik toospecify gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2a13d-324">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="2a13d-325">Örnek:</span><span class="sxs-lookup"><span data-stu-id="2a13d-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="2a13d-326">bir Hive tablosu toouse Avro biçimi, başvurabilirsiniz çok[Apache Hive'nın Öğreticisi](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="2a13d-326">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="2a13d-327">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2a13d-327">Note hello following points:</span></span>  

* <span data-ttu-id="2a13d-328">[Karmaşık veri türlerini](http://avro.apache.org/docs/current/spec.html#schema_complex) desteklenmez (kaydeder, numaralandırmalar, dizileri, haritalar, birleşimler ve sabit).</span><span class="sxs-lookup"><span data-stu-id="2a13d-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="2a13d-329">ORC biçimi</span><span class="sxs-lookup"><span data-stu-id="2a13d-329">ORC format</span></span>
<span data-ttu-id="2a13d-330">Merhaba, tooparse hello ORC dosyaları veya ORC biçiminde hello veri yazmak istiyorsanız ayarlayın `format` `type` özelliği çok**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-330">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="2a13d-331">Merhaba typeProperties bölüm içindeki hello biçimi bölümünde herhangi bir özellik toospecify gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2a13d-331">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="2a13d-332">Örnek:</span><span class="sxs-lookup"><span data-stu-id="2a13d-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="2a13d-333">ORC dosyaları kopyalıyorsanız değil, **olarak-olduğu** şirket içi ve bulut arasında veri depolarına, ağ geçidi makinenizde tooinstall hello JRE 8 (Java Çalışma zamanı ortamı) gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="2a13d-334">64 bit ağ geçidi için 64 bit JRE, 32 bit ağ geçidi için de 32 bit JRE gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="2a13d-335">İki sürüme de [buradan](http://go.microsoft.com/fwlink/?LinkId=808605) ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a13d-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="2a13d-336">Merhaba uygun olanı seçin.</span><span class="sxs-lookup"><span data-stu-id="2a13d-336">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="2a13d-337">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2a13d-337">Note hello following points:</span></span>

* <span data-ttu-id="2a13d-338">Karmaşık veri türleri desteklenmez (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="2a13d-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="2a13d-339">ORC dosyası [sıkıştırmayla ilgili üç seçeneğe sahiptir](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="2a13d-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="2a13d-340">Data Factory, bu sıkıştırma biçimlerinin herhangi birine sahip ORC dosyalarını okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="2a13d-341">Merhaba sıkıştırma kullanır codec olduğu hello meta veri tooread hello verileri.</span><span class="sxs-lookup"><span data-stu-id="2a13d-341">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="2a13d-342">Ancak, tooan ORC dosyasına yazarken, veri fabrikası ZLIB, ORC için hello varsayılan olduğu seçer.</span><span class="sxs-lookup"><span data-stu-id="2a13d-342">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="2a13d-343">Şu anda bu davranış hiçbir seçeneği toooverride yoktur.</span><span class="sxs-lookup"><span data-stu-id="2a13d-343">Currently, there is no option toooverride this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="2a13d-344">Parquet biçimi</span><span class="sxs-lookup"><span data-stu-id="2a13d-344">Parquet format</span></span>
<span data-ttu-id="2a13d-345">Tooparse hello Parquet dosyalarının istediğiniz veya Parquet biçiminde hello veri yazmak istiyorsanız, hello ayarlayın `format` `type` özelliği çok**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-345">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="2a13d-346">Merhaba typeProperties bölüm içindeki hello biçimi bölümünde herhangi bir özellik toospecify gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2a13d-346">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="2a13d-347">Örnek:</span><span class="sxs-lookup"><span data-stu-id="2a13d-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="2a13d-348">Parquet dosyaları kopyalıyorsanız değil, **olarak-olduğu** şirket içi ve bulut arasında veri depolarına, ağ geçidi makinenizde tooinstall hello JRE 8 (Java Çalışma zamanı ortamı) gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="2a13d-349">64 bit ağ geçidi için 64 bit JRE, 32 bit ağ geçidi için de 32 bit JRE gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="2a13d-350">İki sürüme de [buradan](http://go.microsoft.com/fwlink/?LinkId=808605) ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a13d-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="2a13d-351">Merhaba uygun olanı seçin.</span><span class="sxs-lookup"><span data-stu-id="2a13d-351">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="2a13d-352">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2a13d-352">Note hello following points:</span></span>

* <span data-ttu-id="2a13d-353">Karmaşık veri türleri desteklenmez (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="2a13d-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="2a13d-354">Parquet dosya sıkıştırma ilgili seçenekleri aşağıdaki hello vardır: NONE, SNAPPY, GZIP ve LZO.</span><span class="sxs-lookup"><span data-stu-id="2a13d-354">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="2a13d-355">Data Factory, bu sıkıştırma biçimlerinin herhangi birine sahip ORC dosyalarını okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="2a13d-356">Merhaba sıkıştırma codec hello meta veri tooread hello verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="2a13d-356">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="2a13d-357">Ancak, tooa Parquet dosyasına yazarken, veri fabrikası SNAPPY, Parquet biçiminde hello varsayılan olduğu seçer.</span><span class="sxs-lookup"><span data-stu-id="2a13d-357">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="2a13d-358">Şu anda bu davranış hiçbir seçeneği toooverride yoktur.</span><span class="sxs-lookup"><span data-stu-id="2a13d-358">Currently, there is no option toooverride this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="2a13d-359">Sıkıştırma desteği</span><span class="sxs-lookup"><span data-stu-id="2a13d-359">Compression support</span></span>
<span data-ttu-id="2a13d-360">Büyük veri kümeleri işleme g/ç ve ağ performans sorunlarına neden.</span><span class="sxs-lookup"><span data-stu-id="2a13d-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="2a13d-361">Bu nedenle, sıkıştırılmış veri depolarında yazabilir yalnızca hello ağ üzerinden veri aktarımı hızı ve disk alanından tasarruf, ancak ayrıca büyük veri işlerken önemli performans geliştirmeleri getirin.</span><span class="sxs-lookup"><span data-stu-id="2a13d-361">Therefore, compressed data in stores can not only speed up data transfer across hello network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="2a13d-362">Şu anda sıkıştırma, Azure Blob veya şirket içi dosya sistemi gibi dosya tabanlı veri depoları için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2a13d-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="2a13d-363">bir veri kümesi, kullanım hello toospecify sıkıştırma **sıkıştırma** aşağıdaki örneğine hello olduğu gibi JSON hello kümesindeki özelliği:</span><span class="sxs-lookup"><span data-stu-id="2a13d-363">toospecify compression for a dataset, use hello **compression** property in hello dataset JSON as in hello following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="2a13d-364">Merhaba örnek veri kümesi kopyalama etkinliği hello çıkış olarak kullanılan varsayalım hello kopyalama etkinliği sıkıştırır hello GZIP codec ile en iyi oranını kullanarak çıktı verilerini ve hello Azure Blob Storage pagecounts.csv.gz adlı bir dosyaya sıkıştırılmış hello veri yazma.</span><span class="sxs-lookup"><span data-stu-id="2a13d-364">Suppose hello sample dataset is used as hello output of a copy activity, hello copy activity compresses hello output data with GZIP codec using optimal ratio and then write hello compressed data into a file named pagecounts.csv.gz in hello Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="2a13d-365">Merhaba veri sıkıştırma ayarları desteklenmez **AvroFormat**, **OrcFormat**, veya **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-365">Compression settings are not supported for data in hello **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="2a13d-366">Bu biçimler dosyalarında okurken, veri fabrikası algılar ve hello sıkıştırma codec hello meta verilerde kullanır.</span><span class="sxs-lookup"><span data-stu-id="2a13d-366">When reading files in these formats, Data Factory detects and uses hello compression codec in hello metadata.</span></span> <span data-ttu-id="2a13d-367">Toofiles aşağıdaki biçimlerde yazarken, veri fabrikası hello varsayılan sıkıştırma codec Bu biçim seçer.</span><span class="sxs-lookup"><span data-stu-id="2a13d-367">When writing toofiles in these formats, Data Factory chooses hello default compression codec for that format.</span></span> <span data-ttu-id="2a13d-368">Örneğin, ZLIB OrcFormat ve ParquetFormat SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="2a13d-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="2a13d-369">Merhaba **sıkıştırma** bölüm iki özellik vardır:</span><span class="sxs-lookup"><span data-stu-id="2a13d-369">hello **compression** section has two properties:</span></span>  

* <span data-ttu-id="2a13d-370">**Tür:** olabilir hello sıkıştırma codec **GZIP**, **Deflate**, **bzıp2**, veya **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-370">**Type:** hello compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="2a13d-371">**Düzeyi:** olabilir hello sıkıştırma oranı **Optimal** veya **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="2a13d-371">**Level:** hello compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="2a13d-372">**Hızlı:** hello sıkıştırma işlemini tamamlamanız gereken mümkün olan en kısa sürede hello elde edilen dosyası en iyi şekilde sıkıştırılmaz olsa bile.</span><span class="sxs-lookup"><span data-stu-id="2a13d-372">**Fastest:** hello compression operation should complete as quickly as possible, even if hello resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="2a13d-373">**En iyi**: hello sıkıştırma işlemi en iyi şekilde sıkıştırılmış, dahi hello işlemi daha uzun bir süre toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="2a13d-373">**Optimal**: hello compression operation should be optimally compressed, even if hello operation takes a longer time toocomplete.</span></span>

    <span data-ttu-id="2a13d-374">Daha fazla bilgi için bkz: [sıkıştırma düzeyi](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="2a13d-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="2a13d-375">Belirttiğinizde `compression` bir girdi veri kümesi JSON özelliğinde hello ardışık düzen hello kaynağından; sıkıştırılmış verileri okuyabilir ve bir çıkış dataset JSON hello özelliğini belirttiğinizde hello kopyalama etkinliği sıkıştırılmış veri toohello hedef yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a13d-375">When you specify `compression` property in an input dataset JSON, hello pipeline can read compressed data from hello source; and when you specify hello property in an output dataset JSON, hello copy activity can write compressed data toohello destination.</span></span> <span data-ttu-id="2a13d-376">Bazı örnek senaryolar verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2a13d-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="2a13d-377">GZIP sıkıştırılmış verileri Azure blob'tan okuma, iptal ve sonuç verileri tooan Azure SQL veritabanı yazma.</span><span class="sxs-lookup"><span data-stu-id="2a13d-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data tooan Azure SQL database.</span></span> <span data-ttu-id="2a13d-378">Merhaba giriş Azure Blob kümesiyle hello tanımladığınız `compression` `type` JSON özellik GZIP olarak.</span><span class="sxs-lookup"><span data-stu-id="2a13d-378">You define hello input Azure Blob dataset with hello `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="2a13d-379">Şirket içi dosya sistemi düz metin dosyasından veri okunamıyor, GZip biçimi kullanarak Sıkıştır ve sıkıştırılmış hello veri tooan Azure blob yazma.</span><span class="sxs-lookup"><span data-stu-id="2a13d-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write hello compressed data tooan Azure blob.</span></span> <span data-ttu-id="2a13d-380">Merhaba çıktı Azure Blob kümesiyle tanımladığınız `compression` `type` JSON özellik GZip olarak.</span><span class="sxs-lookup"><span data-stu-id="2a13d-380">You define an output Azure Blob dataset with hello `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="2a13d-381">FTP sunucusu, .zip dosyasından okuma içindeki tooget hello dosyaları sıkıştırılmış ve bu dosyaların Azure Data Lake Store güden.</span><span class="sxs-lookup"><span data-stu-id="2a13d-381">Read .zip file from FTP server, decompress it tooget hello files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="2a13d-382">Girdi bir FTP veri kümesi'hello ile tanımladığınız `compression` `type` JSON özelliği ZipDeflate olarak.</span><span class="sxs-lookup"><span data-stu-id="2a13d-382">You define an input FTP dataset with hello `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="2a13d-383">GZIP sıkıştırılmış verileri Azure blob'tan okuma, iptal, bzıp2 kullanarak Sıkıştır ve sonuç verileri tooan Azure blob yazma.</span><span class="sxs-lookup"><span data-stu-id="2a13d-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data tooan Azure blob.</span></span> <span data-ttu-id="2a13d-384">Merhaba giriş Azure Blob kümesiyle tanımladığınız `compression` `type` tooGZIP ayarlayın ve çıktı veri kümesi ile Merhaba `compression` `type` tooBZIP2 bu durumda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2a13d-384">You define hello input Azure Blob dataset with `compression` `type` set tooGZIP and hello output dataset with `compression` `type` set tooBZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="2a13d-385">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a13d-385">Next steps</span></span>
<span data-ttu-id="2a13d-386">Aşağıdaki makaleler Azure Data Factory ile desteklenen dosya tabanlı veri depoları için hello bakın:</span><span class="sxs-lookup"><span data-stu-id="2a13d-386">See hello following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="2a13d-387">Azure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="2a13d-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="2a13d-388">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="2a13d-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="2a13d-389">FTP</span><span class="sxs-lookup"><span data-stu-id="2a13d-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="2a13d-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="2a13d-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="2a13d-391">Dosya Sistemi</span><span class="sxs-lookup"><span data-stu-id="2a13d-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="2a13d-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="2a13d-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
