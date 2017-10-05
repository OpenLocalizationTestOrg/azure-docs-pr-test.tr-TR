---
title: "Azure Data Factory dosya ve sıkıştırma biçimlerde | Microsoft Docs"
description: "Azure Data Factory ile desteklenen dosya biçimleri hakkında bilgi edinin."
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
ms.openlocfilehash: f4746e0dd249e417b8077a9bc733d2886daafdf2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="08529-104">Azure Data Factory tarafından desteklenen dosya ve sıkıştırma biçimleri</span><span class="sxs-lookup"><span data-stu-id="08529-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="08529-105">*Bu konu, aşağıdaki bağlayıcılar için geçerlidir: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [dosya sistemi](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), ve [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="08529-105">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="08529-106">Azure Data Factory aşağıdaki dosya biçimi türlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="08529-106">Azure Data Factory supports the following file format types:</span></span>

* [<span data-ttu-id="08529-107">Metin biçimi</span><span class="sxs-lookup"><span data-stu-id="08529-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="08529-108">JSON biçimi</span><span class="sxs-lookup"><span data-stu-id="08529-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="08529-109">Avro biçimi</span><span class="sxs-lookup"><span data-stu-id="08529-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="08529-110">ORC biçimi</span><span class="sxs-lookup"><span data-stu-id="08529-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="08529-111">Parquet biçimi</span><span class="sxs-lookup"><span data-stu-id="08529-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="08529-112">Metin biçimi</span><span class="sxs-lookup"><span data-stu-id="08529-112">Text format</span></span>
<span data-ttu-id="08529-113">Bir metin dosyasından okuma veya bir metin dosyasına yazma istiyorsanız, `type` özelliğinde `format` kümesine bölümünü **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="08529-113">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="08529-114">İsterseniz `format` bölümünde aşağıdaki **isteğe bağlı** özellikleri de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-114">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="08529-115">Yapılandırma adımları için [TextFormat örneği](#textformat-example) bölümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="08529-115">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="08529-116">Özellik</span><span class="sxs-lookup"><span data-stu-id="08529-116">Property</span></span> | <span data-ttu-id="08529-117">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08529-117">Description</span></span> | <span data-ttu-id="08529-118">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="08529-118">Allowed values</span></span> | <span data-ttu-id="08529-119">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08529-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08529-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="08529-120">columnDelimiter</span></span> |<span data-ttu-id="08529-121">Bir dosyadaki sütunları ayırmak için kullanılan karakterdir.</span><span class="sxs-lookup"><span data-stu-id="08529-121">The character used to separate columns in a file.</span></span> <span data-ttu-id="08529-122">Verilerinizde büyük olasılıkla yok nadir bir yazdırılamayan char kullanmayı düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-122">You can consider to use a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="08529-123">Örneğin, Başlat, başlık (SOH) temsil eder "\u0001" belirtin.</span><span class="sxs-lookup"><span data-stu-id="08529-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="08529-124">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="08529-124">Only one character is allowed.</span></span> <span data-ttu-id="08529-125">**Varsayılan** değer **virgül (",")** olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="08529-125">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="08529-126">Bir Unicode karakteri kullanmak için başvurmak [Unicode karakterler](https://en.wikipedia.org/wiki/List_of_Unicode_characters) ilgili kod elde edin.</span><span class="sxs-lookup"><span data-stu-id="08529-126">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="08529-127">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-127">No</span></span> |
| <span data-ttu-id="08529-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="08529-128">rowDelimiter</span></span> |<span data-ttu-id="08529-129">Bir dosyadaki satırları ayırmak için kullanılan karakterdir.</span><span class="sxs-lookup"><span data-stu-id="08529-129">The character used to separate rows in a file.</span></span> |<span data-ttu-id="08529-130">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="08529-130">Only one character is allowed.</span></span> <span data-ttu-id="08529-131">**Varsayılan** değer, okuma sırasında **["\r\n", "\r", "\n"]** değerlerinden biri, yazma sırasında ise **"\r\n"** olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="08529-131">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="08529-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-132">No</span></span> |
| <span data-ttu-id="08529-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="08529-133">escapeChar</span></span> |<span data-ttu-id="08529-134">Giriş dosyasının içeriğindeki bir sütun ayırıcısına kaçış karakteri eklemek için kullanılan özel karakterdir.</span><span class="sxs-lookup"><span data-stu-id="08529-134">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="08529-135">Bir tablo için hem escapeChar hem de quoteChar parametrelerini aynı anda belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="08529-136">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="08529-136">Only one character is allowed.</span></span> <span data-ttu-id="08529-137">Varsayılan değer yoktur.</span><span class="sxs-lookup"><span data-stu-id="08529-137">No default value.</span></span> <br/><br/><span data-ttu-id="08529-138">Örnek: Sütun sınırlayıcınız virgül (",") karakteriyse ancak metin içinde virgül karakteri kullanılıyorsa (örneğin: "Merhaba, dünya"), "$" karakterini kaçış karakteri olarak tanımlayabilir ve kaynakta "Merhaba$, dünya" dizesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-138">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="08529-139">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-139">No</span></span> |
| <span data-ttu-id="08529-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="08529-140">quoteChar</span></span> |<span data-ttu-id="08529-141">Bir dize değerini tırnak içine almak için kullanılan karakterdir.</span><span class="sxs-lookup"><span data-stu-id="08529-141">The character used to quote a string value.</span></span> <span data-ttu-id="08529-142">Tırnak işareti içindeki sütun ve satır sınırlayıcıları, dize değerinin bir parçası olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="08529-142">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="08529-143">Bu özellik hem giriş hem de çıkış veri kümelerine uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="08529-143">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="08529-144">Bir tablo için hem escapeChar hem de quoteChar parametrelerini aynı anda belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="08529-145">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="08529-145">Only one character is allowed.</span></span> <span data-ttu-id="08529-146">Varsayılan değer yoktur.</span><span class="sxs-lookup"><span data-stu-id="08529-146">No default value.</span></span> <br/><br/><span data-ttu-id="08529-147">Örneğin, sütun sınırlayıcınız virgül (",") karakteriyse ancak metin içinde virgül karakteri kullanılıyorsa (örneğin: <Merhaba, dünya>), " (çift tırnak) karakterini tırnak karakteri olarak tanımlayabilir ve kaynakta "Merhaba, dünya" dizesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-147">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="08529-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-148">No</span></span> |
| <span data-ttu-id="08529-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="08529-149">nullValue</span></span> |<span data-ttu-id="08529-150">Bir null değeri temsil etmek için kullanılan bir veya daha fazla karakterdir.</span><span class="sxs-lookup"><span data-stu-id="08529-150">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="08529-151">Bir veya daha fazla karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="08529-151">One or more characters.</span></span> <span data-ttu-id="08529-152">**Varsayılan** değerler okuma sırasında **"\N" ve "NULL"**, yazma sırasında ise **"\N"** olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="08529-152">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="08529-153">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-153">No</span></span> |
| <span data-ttu-id="08529-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="08529-154">encodingName</span></span> |<span data-ttu-id="08529-155">Kodlama adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="08529-155">Specify the encoding name.</span></span> |<span data-ttu-id="08529-156">Geçerli bir kodlama adı.</span><span class="sxs-lookup"><span data-stu-id="08529-156">A valid encoding name.</span></span> <span data-ttu-id="08529-157">Bkz. [Encoding.EncodingName Özelliği](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="08529-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="08529-158">Örnek: windows-1250 veya shift_jis.</span><span class="sxs-lookup"><span data-stu-id="08529-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="08529-159">**Varsayılan** değer **UTF-8** olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="08529-159">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="08529-160">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-160">No</span></span> |
| <span data-ttu-id="08529-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="08529-161">firstRowAsHeader</span></span> |<span data-ttu-id="08529-162">İlk satırın üst bilgi olarak kabul edilip edilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="08529-162">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="08529-163">Giriş veri kümesinde Data Factory ilk satırı üst bilgi olarak okur.</span><span class="sxs-lookup"><span data-stu-id="08529-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="08529-164">Çıkış veri kümesinde Data Factory ilk satırı üst bilgi olarak yazar.</span><span class="sxs-lookup"><span data-stu-id="08529-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="08529-165">Örnek senaryolar için bkz. [`firstRowAsHeader` ve `skipLineCount` kullanım senaryoları](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="08529-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="08529-166">True</span><span class="sxs-lookup"><span data-stu-id="08529-166">True</span></span><br/><span data-ttu-id="08529-167"><b>False (varsayılan)</b></span><span class="sxs-lookup"><span data-stu-id="08529-167"><b>False (default)</b></span></span> |<span data-ttu-id="08529-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-168">No</span></span> |
| <span data-ttu-id="08529-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="08529-169">skipLineCount</span></span> |<span data-ttu-id="08529-170">Giriş dosyalarından okuma sırasında atlanacak satır sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="08529-170">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="08529-171">Hem skipLineCount hem de firstRowAsHeader parametresi belirtilirse önce satırlar atlanır, ardından giriş dosyasındaki üst bilgi bilgileri okunur.</span><span class="sxs-lookup"><span data-stu-id="08529-171">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="08529-172">Örnek senaryolar için bkz. [`firstRowAsHeader` ve `skipLineCount` kullanım senaryoları](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="08529-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="08529-173">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="08529-173">Integer</span></span> |<span data-ttu-id="08529-174">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-174">No</span></span> |
| <span data-ttu-id="08529-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="08529-175">treatEmptyAsNull</span></span> |<span data-ttu-id="08529-176">Bir giriş dosyasından veri okuma sırasında null veya boş dizenin null değer olarak kabul edilip edilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="08529-176">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="08529-177">**True (varsayılan)**</span><span class="sxs-lookup"><span data-stu-id="08529-177">**True (default)**</span></span><br/><span data-ttu-id="08529-178">False</span><span class="sxs-lookup"><span data-stu-id="08529-178">False</span></span> |<span data-ttu-id="08529-179">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="08529-180">TextFormat örneği</span><span class="sxs-lookup"><span data-stu-id="08529-180">TextFormat example</span></span>
<span data-ttu-id="08529-181">Bir veri kümesi için aşağıdaki JSON tanımında bazı isteğe bağlı özellikler belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="08529-181">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

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

<span data-ttu-id="08529-182">`quoteChar` yerine `escapeChar` kullanmak için `quoteChar` yazan satırı şu escapeChar ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="08529-182">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="08529-183">firstRowAsHeader ve skipLineCount kullanım senaryoları</span><span class="sxs-lookup"><span data-stu-id="08529-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="08529-184">Dosya olmayan bir kaynaktan bir metin dosyasına kopyalama yapıyorsunuz ve şema meta verilerini (örneğin, SQL şeması) içeren bir üst bilgi satırı eklemek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="08529-184">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="08529-185">Bu senaryo için çıkış veri kümesinde `firstRowAsHeader` parametresini true olarak belirleyin.</span><span class="sxs-lookup"><span data-stu-id="08529-185">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="08529-186">Üst bilgi satırı içeren bir metin dosyasından dosya olmayan bir havuza kopyalama yapıyorsunuz ve üst bilgi satırını almak istemiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="08529-186">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="08529-187">Giriş veri kümesinde `firstRowAsHeader` parametresini true olarak belirleyin.</span><span class="sxs-lookup"><span data-stu-id="08529-187">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="08529-188">Bir metin dosyasından kopyalama yapıyorsunuz ve dosyanın başındaki veri içermeyen veya üst bilgi bilgilerini içeren birkaç satırı atlamak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="08529-188">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="08529-189">Atlanacak satır sayısını belirtmek için `skipLineCount` değerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="08529-189">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="08529-190">Dosyanın geri kalan kısmında üst bilgi satırı varsa `firstRowAsHeader` değerini de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-190">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="08529-191">Hem `skipLineCount` hem de `firstRowAsHeader` parametresi belirtilirse önce satırlar atlanır, ardından giriş dosyasındaki üst bilgi bilgileri okunur.</span><span class="sxs-lookup"><span data-stu-id="08529-191">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="08529-192">JSON biçimi</span><span class="sxs-lookup"><span data-stu-id="08529-192">JSON format</span></span>
<span data-ttu-id="08529-193">İçin **bir JSON dosyası olarak içeri/dışarı aktarma-olduğu içine/Azure Cosmos DB'den**, bkz: [içeri/dışarı aktarma JSON belgeleri](data-factory-azure-documentdb-connector.md#importexport-json-documents) bölümüne [/Azure Cosmos DB'den veri taşıma](data-factory-azure-documentdb-connector.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="08529-193">To **import/export a JSON file as-is into/from Azure Cosmos DB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="08529-194">JSON dosyaları ayrıştırma veya JSON biçiminde veri yazmak istiyorsanız, Ayarla `type` özelliğinde `format` için bölüm **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="08529-194">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="08529-195">İsterseniz `format` bölümünde aşağıdaki **isteğe bağlı** özellikleri de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-195">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="08529-196">Yapılandırma adımları için [JsonFormat örneği](#jsonformat-example) bölümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="08529-196">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="08529-197">Özellik</span><span class="sxs-lookup"><span data-stu-id="08529-197">Property</span></span> | <span data-ttu-id="08529-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="08529-198">Description</span></span> | <span data-ttu-id="08529-199">Gerekli</span><span class="sxs-lookup"><span data-stu-id="08529-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08529-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="08529-200">filePattern</span></span> |<span data-ttu-id="08529-201">Her bir JSON dosyasında depolanan verilerin desenini belirtir.</span><span class="sxs-lookup"><span data-stu-id="08529-201">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="08529-202">İzin verilen değerler: **setOfObjects** ve **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="08529-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="08529-203">**Varsayılan** değer **setOfObjects** olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="08529-203">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="08529-204">Bu desenler hakkında ayrıntılı bilgi için bkz. [JSON dosyası desenleri](#json-file-patterns).</span><span class="sxs-lookup"><span data-stu-id="08529-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="08529-205">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-205">No</span></span> |
| <span data-ttu-id="08529-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="08529-206">jsonNodeReference</span></span> | <span data-ttu-id="08529-207">Bir dizi alanındaki aynı desene sahip verileri yinelemek ve ayıklamak istiyorsanız o dizinin JSON yolunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="08529-207">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="08529-208">Bu özellik yalnızca JSON dosyalarından veri kopyalarken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="08529-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="08529-209">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-209">No</span></span> |
| <span data-ttu-id="08529-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="08529-210">jsonPathDefinition</span></span> | <span data-ttu-id="08529-211">Her sütun için JSON yolu ifadesini belirtin ve özel bir sütun adıyla eşleyin (küçük harfle başlatın).</span><span class="sxs-lookup"><span data-stu-id="08529-211">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="08529-212">Bu özellik yalnızca JSON dosyalarından veri kopyalarken desteklenir. Verileri nesne veya diziden ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="08529-213">Kök nesne altındaki alanlar için root $ ile, `jsonNodeReference` özelliği tarafından seçilen dizinin içindeki alanlar için ise dizi öğesiyle başlayın.</span><span class="sxs-lookup"><span data-stu-id="08529-213">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="08529-214">Yapılandırma adımları için [JsonFormat örneği](#jsonformat-example) bölümünü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="08529-214">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="08529-215">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-215">No</span></span> |
| <span data-ttu-id="08529-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="08529-216">encodingName</span></span> |<span data-ttu-id="08529-217">Kodlama adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="08529-217">Specify the encoding name.</span></span> <span data-ttu-id="08529-218">Geçerli kodlama adlarının listesi için bkz. [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Özelliği.</span><span class="sxs-lookup"><span data-stu-id="08529-218">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="08529-219">Örneğin: windows-1250 veya shift_jis.</span><span class="sxs-lookup"><span data-stu-id="08529-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="08529-220">**Varsayılan** değer **UTF-8** olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="08529-220">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="08529-221">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-221">No</span></span> |
| <span data-ttu-id="08529-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="08529-222">nestingSeparator</span></span> |<span data-ttu-id="08529-223">İç içe geçme düzeylerini ayırmak için kullanılan karakterdir.</span><span class="sxs-lookup"><span data-stu-id="08529-223">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="08529-224">Varsayılan değer "." (nokta) olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="08529-224">The default value is '.' (dot).</span></span> |<span data-ttu-id="08529-225">Hayır</span><span class="sxs-lookup"><span data-stu-id="08529-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="08529-226">JSON dosyası desenleri</span><span class="sxs-lookup"><span data-stu-id="08529-226">JSON file patterns</span></span>

<span data-ttu-id="08529-227">Kopyalama etkinliği, JSON dosyalarınızın aşağıdaki desenleri ayrıştırma yapabilir:</span><span class="sxs-lookup"><span data-stu-id="08529-227">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="08529-228">**1. Tür: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="08529-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="08529-229">Her dosya tek bir nesne veya satırlara ayrılmış/bitiştirilmiş birden fazla nesne içerir.</span><span class="sxs-lookup"><span data-stu-id="08529-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="08529-230">Bu seçenek bir çıkış veri kümesinde belirlendiğinde, kopyalama etkinliği her satırda bir nesnenin bulunduğu (satırlara ayrılmış) tek bir JSON dosyası üretir.</span><span class="sxs-lookup"><span data-stu-id="08529-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="08529-231">**tek nesne JSON örneği**</span><span class="sxs-lookup"><span data-stu-id="08529-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="08529-232">**satırlara ayrılmış JSON örneği**</span><span class="sxs-lookup"><span data-stu-id="08529-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="08529-233">**bitiştirilmiş JSON örneği**</span><span class="sxs-lookup"><span data-stu-id="08529-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="08529-234">**2. Tür: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="08529-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="08529-235">Her dosya bir nesne dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="08529-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="08529-236">JsonFormat örneği</span><span class="sxs-lookup"><span data-stu-id="08529-236">JsonFormat example</span></span>

<span data-ttu-id="08529-237">**Örnek Durum 1: JSON dosyalarından veri kopyalama**</span><span class="sxs-lookup"><span data-stu-id="08529-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="08529-238">Aşağıdaki iki örnek verileri JSON dosyaları kopyalarken bakın.</span><span class="sxs-lookup"><span data-stu-id="08529-238">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="08529-239">Dikkat edilecek genel noktalar:</span><span class="sxs-lookup"><span data-stu-id="08529-239">The generic points to note:</span></span>

<span data-ttu-id="08529-240">**Örnek 1: nesne ve diziden veri ayıklama**</span><span class="sxs-lookup"><span data-stu-id="08529-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="08529-241">Bu örnekte, bir kök JSON nesnesinin tablosal sonuçtaki tek bir kayıtla eşleşmesi beklenir.</span><span class="sxs-lookup"><span data-stu-id="08529-241">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="08529-242">Aşağıdaki içeriğe sahip bir JSON dosyanız varsa:</span><span class="sxs-lookup"><span data-stu-id="08529-242">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="08529-243">ve hem nesne hem de diziden veri ayıklayarak bir Azure SQL tablosuna aşağıdaki biçimde kopyalamak istersiniz:</span><span class="sxs-lookup"><span data-stu-id="08529-243">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="08529-244">id</span><span class="sxs-lookup"><span data-stu-id="08529-244">id</span></span> | <span data-ttu-id="08529-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="08529-245">deviceType</span></span> | <span data-ttu-id="08529-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="08529-246">targetResourceType</span></span> | <span data-ttu-id="08529-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="08529-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="08529-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="08529-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="08529-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="08529-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="08529-250">PC</span><span class="sxs-lookup"><span data-stu-id="08529-250">PC</span></span> | <span data-ttu-id="08529-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="08529-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="08529-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="08529-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="08529-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="08529-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="08529-254">**JsonFormat** türüne sahip giriş veri kümesi şu şekilde tanımlanır: (yalnızca ilgili bölümlerin gösterildiği kısmi tanım).</span><span class="sxs-lookup"><span data-stu-id="08529-254">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="08529-255">Daha ayrıntılı belirtmek gerekirse:</span><span class="sxs-lookup"><span data-stu-id="08529-255">More specifically:</span></span>

- <span data-ttu-id="08529-256">`structure` bölümü, tablo verilerine dönüştürme sırasında kullanılan özelleştirilmiş sütun adlarını ve karşılık gelen veri türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="08529-256">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="08529-257">Bu bölüm **isteğe bağlıdır** ve yalnızca sütun eşleme için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08529-257">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="08529-258">Bkz: [kaynak veri kümesi sütunları hedef veri kümesi sütun eşleme](data-factory-map-columns.md) daha fazla ayrıntı için bölüm.</span><span class="sxs-lookup"><span data-stu-id="08529-258">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="08529-259">`jsonPathDefinition`, her sütun için verilerin ayıklanacağı JSON yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="08529-259">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="08529-260">Verileri diziden kopyalamak için **array[x].property** öğesini kullanarak söz konusu özelliğin değerini xth nesnesinden ayıklayabilir veya **array[*].property** öğesini kullanarak bu özelliği içeren herhangi bir nesneden değeri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-260">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="08529-261">**Örnek 2: diziden aynı desene sahip birden fazla nesneyi çapraz uygulama**</span><span class="sxs-lookup"><span data-stu-id="08529-261">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="08529-262">Bu örnekte, bir kök JSON nesnesinin tablosal sonuçtaki birden fazla kayda dönüştürülmesi beklenir.</span><span class="sxs-lookup"><span data-stu-id="08529-262">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="08529-263">Aşağıdaki içeriğe sahip bir JSON dosyanız varsa:</span><span class="sxs-lookup"><span data-stu-id="08529-263">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="08529-264">ve bunu bir Azure SQL tablosuna aşağıdaki biçimde, dizi içindeki verileri düzleştirerek ve ortak kök bilgileriyle çapraz birleşim yaparak kopyalamak istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="08529-264">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="08529-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="08529-265">ordernumber</span></span> | <span data-ttu-id="08529-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="08529-266">orderdate</span></span> | <span data-ttu-id="08529-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="08529-267">order_pd</span></span> | <span data-ttu-id="08529-268">order_price</span><span class="sxs-lookup"><span data-stu-id="08529-268">order_price</span></span> | <span data-ttu-id="08529-269">city</span><span class="sxs-lookup"><span data-stu-id="08529-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="08529-270">01</span><span class="sxs-lookup"><span data-stu-id="08529-270">01</span></span> | <span data-ttu-id="08529-271">20170122</span><span class="sxs-lookup"><span data-stu-id="08529-271">20170122</span></span> | <span data-ttu-id="08529-272">P1</span><span class="sxs-lookup"><span data-stu-id="08529-272">P1</span></span> | <span data-ttu-id="08529-273">23</span><span class="sxs-lookup"><span data-stu-id="08529-273">23</span></span> | <span data-ttu-id="08529-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="08529-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="08529-275">01</span><span class="sxs-lookup"><span data-stu-id="08529-275">01</span></span> | <span data-ttu-id="08529-276">20170122</span><span class="sxs-lookup"><span data-stu-id="08529-276">20170122</span></span> | <span data-ttu-id="08529-277">P2</span><span class="sxs-lookup"><span data-stu-id="08529-277">P2</span></span> | <span data-ttu-id="08529-278">13</span><span class="sxs-lookup"><span data-stu-id="08529-278">13</span></span> | <span data-ttu-id="08529-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="08529-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="08529-280">01</span><span class="sxs-lookup"><span data-stu-id="08529-280">01</span></span> | <span data-ttu-id="08529-281">20170122</span><span class="sxs-lookup"><span data-stu-id="08529-281">20170122</span></span> | <span data-ttu-id="08529-282">P3</span><span class="sxs-lookup"><span data-stu-id="08529-282">P3</span></span> | <span data-ttu-id="08529-283">231</span><span class="sxs-lookup"><span data-stu-id="08529-283">231</span></span> | <span data-ttu-id="08529-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="08529-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="08529-285">**JsonFormat** türüne sahip giriş veri kümesi şu şekilde tanımlanır: (yalnızca ilgili bölümlerin gösterildiği kısmi tanım).</span><span class="sxs-lookup"><span data-stu-id="08529-285">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="08529-286">Daha ayrıntılı belirtmek gerekirse:</span><span class="sxs-lookup"><span data-stu-id="08529-286">More specifically:</span></span>

- <span data-ttu-id="08529-287">`structure` bölümü, tablo verilerine dönüştürme sırasında kullanılan özelleştirilmiş sütun adlarını ve karşılık gelen veri türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="08529-287">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="08529-288">Bu bölüm **isteğe bağlıdır** ve yalnızca sütun eşleme için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08529-288">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="08529-289">Bkz: [kaynak veri kümesi sütunları hedef veri kümesi sütun eşleme](data-factory-map-columns.md) daha fazla ayrıntı için bölüm.</span><span class="sxs-lookup"><span data-stu-id="08529-289">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="08529-290">`jsonNodeReference`, **dizi** sipariş satırlarının altında aynı desene sahip nesnelerdeki verilerin yineleneceğini ve ayıklanacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="08529-290">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="08529-291">`jsonPathDefinition`, her sütun için verilerin ayıklanacağı JSON yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="08529-291">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="08529-292">Bu örnekte "ordernumber", "orderdate" ve "city", kök nesnenin altında ve "$." ile başlayan JSON yolundayken, "order_pd" ve "order_price", "$." olmadan dizi öğesinden türetilen yol kullanılarak tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="08529-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="08529-293">**Aşağıdaki noktalara dikkat edin:**</span><span class="sxs-lookup"><span data-stu-id="08529-293">**Note the following points:**</span></span>

* <span data-ttu-id="08529-294">`structure` ve `jsonPathDefinition`, Data Factory veri kümesinde tanımlanmamışsa, Copy Activity şemayı ilk nesneden algılar ve nesnenin tamamını düzleştirir.</span><span class="sxs-lookup"><span data-stu-id="08529-294">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="08529-295">JSON girişi bir diziye sahipse, Copy Activity dizi değerinin tamamını varsayılan olarak bir dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="08529-295">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="08529-296">Verileri `jsonNodeReference` ve/veya `jsonPathDefinition` kullanarak ayıklayabilir ya da `jsonPathDefinition` içinde belirtmeden atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-296">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="08529-297">Aynı düzeyde birden fazla ad varsa Copy Activity sonuncusunu alır.</span><span class="sxs-lookup"><span data-stu-id="08529-297">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="08529-298">Özellik adları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="08529-298">Property names are case-sensitive.</span></span> <span data-ttu-id="08529-299">Aynı ada ancak farklı büyük/küçük harf düzenine sahip iki özellik, iki ayrı özellik olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="08529-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="08529-300">**Durum 2: JSON dosyasına veri yazma**</span><span class="sxs-lookup"><span data-stu-id="08529-300">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="08529-301">Aşağıdaki tabloda SQL veritabanında varsa:</span><span class="sxs-lookup"><span data-stu-id="08529-301">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="08529-302">id</span><span class="sxs-lookup"><span data-stu-id="08529-302">id</span></span> | <span data-ttu-id="08529-303">order_date</span><span class="sxs-lookup"><span data-stu-id="08529-303">order_date</span></span> | <span data-ttu-id="08529-304">order_price</span><span class="sxs-lookup"><span data-stu-id="08529-304">order_price</span></span> | <span data-ttu-id="08529-305">order_by</span><span class="sxs-lookup"><span data-stu-id="08529-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="08529-306">1</span><span class="sxs-lookup"><span data-stu-id="08529-306">1</span></span> | <span data-ttu-id="08529-307">20170119</span><span class="sxs-lookup"><span data-stu-id="08529-307">20170119</span></span> | <span data-ttu-id="08529-308">2000</span><span class="sxs-lookup"><span data-stu-id="08529-308">2000</span></span> | <span data-ttu-id="08529-309">David</span><span class="sxs-lookup"><span data-stu-id="08529-309">David</span></span> |
| <span data-ttu-id="08529-310">2</span><span class="sxs-lookup"><span data-stu-id="08529-310">2</span></span> | <span data-ttu-id="08529-311">20170120</span><span class="sxs-lookup"><span data-stu-id="08529-311">20170120</span></span> | <span data-ttu-id="08529-312">3500</span><span class="sxs-lookup"><span data-stu-id="08529-312">3500</span></span> | <span data-ttu-id="08529-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="08529-313">Patrick</span></span> |
| <span data-ttu-id="08529-314">3</span><span class="sxs-lookup"><span data-stu-id="08529-314">3</span></span> | <span data-ttu-id="08529-315">20170121</span><span class="sxs-lookup"><span data-stu-id="08529-315">20170121</span></span> | <span data-ttu-id="08529-316">4000</span><span class="sxs-lookup"><span data-stu-id="08529-316">4000</span></span> | <span data-ttu-id="08529-317">Jason</span><span class="sxs-lookup"><span data-stu-id="08529-317">Jason</span></span> |

<span data-ttu-id="08529-318">ve aşağıdaki biçimde bir JSON nesnesi yazmak beklediğiniz her kayıt için:</span><span class="sxs-lookup"><span data-stu-id="08529-318">and for each record, you expect to write to a JSON object in the following format:</span></span>
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

<span data-ttu-id="08529-319">**JsonFormat** türüne sahip çıkış veri kümesi şu şekilde tanımlanır: (yalnızca ilgili bölümlerin gösterildiği kısmi tanım).</span><span class="sxs-lookup"><span data-stu-id="08529-319">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="08529-320">Daha belirgin olarak `structure` bölüm hedef dosyasında özelleştirilmiş özellik adlarını tanımlar `nestingSeparator` (varsayılan değer ".") adı iç içe katmandan tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="08529-320">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="08529-321">Bu bölüm **isteğe bağlıdır** ve kaynak sütunu adıyla karşılaştırarak özellik adını değiştirmek veya özelliklerin bazılarını iç içe yerleştirmek için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08529-321">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="08529-322">AVRO biçimi</span><span class="sxs-lookup"><span data-stu-id="08529-322">AVRO format</span></span>
<span data-ttu-id="08529-323">Avro dosyalarını ayrıştırmak veya verileri Avro biçiminde yazmak istiyorsanız `format` `type` özelliğini **AvroFormat** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="08529-323">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="08529-324">typeProperties bölümünün içindeki Format bölümünde herhangi bir özellik belirtmenize gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="08529-324">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="08529-325">Örnek:</span><span class="sxs-lookup"><span data-stu-id="08529-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="08529-326">Avro biçimini bir Hive tablosunda kullanmak için [Apache Hive öğreticisini](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe) inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-326">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="08529-327">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="08529-327">Note the following points:</span></span>  

* <span data-ttu-id="08529-328">[Karmaşık veri türlerini](http://avro.apache.org/docs/current/spec.html#schema_complex) desteklenmez (kaydeder, numaralandırmalar, dizileri, haritalar, birleşimler ve sabit).</span><span class="sxs-lookup"><span data-stu-id="08529-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="08529-329">ORC biçimi</span><span class="sxs-lookup"><span data-stu-id="08529-329">ORC format</span></span>
<span data-ttu-id="08529-330">ORC dosyalarını ayrıştırmak veya verileri ORC biçiminde yazmak istiyorsanız `format` `type` özelliğini **OrcFormat** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="08529-330">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="08529-331">typeProperties bölümünün içindeki Format bölümünde herhangi bir özellik belirtmenize gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="08529-331">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="08529-332">Örnek:</span><span class="sxs-lookup"><span data-stu-id="08529-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="08529-333">Şirket içi ve bulut veri depoları arasında ORC dosyalarını **olduğu gibi** kopyalamıyorsanız, ağ geçidi cihazınıza JRE 8 (Java Çalışma Zamanı Ortamı) yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="08529-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="08529-334">64 bit ağ geçidi için 64 bit JRE, 32 bit ağ geçidi için de 32 bit JRE gerekir.</span><span class="sxs-lookup"><span data-stu-id="08529-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="08529-335">İki sürüme de [buradan](http://go.microsoft.com/fwlink/?LinkId=808605) ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="08529-336">Cihazınıza uygun olanı seçin.</span><span class="sxs-lookup"><span data-stu-id="08529-336">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="08529-337">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="08529-337">Note the following points:</span></span>

* <span data-ttu-id="08529-338">Karmaşık veri türleri desteklenmez (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="08529-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="08529-339">ORC dosyası [sıkıştırmayla ilgili üç seçeneğe sahiptir](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="08529-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="08529-340">Data Factory, bu sıkıştırma biçimlerinin herhangi birine sahip ORC dosyalarını okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="08529-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="08529-341">Verileri okumak için meta verilerdeki sıkıştırma kodlayıcısı/kod çözücüsünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="08529-341">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="08529-342">Ancak Data Factory bir ORC dosyasına yazarken varsayılan ORC değeri olan ZLIB seçeneğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="08529-342">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="08529-343">Şu anda bu davranışı geçersiz kılma seçeneği yoktur.</span><span class="sxs-lookup"><span data-stu-id="08529-343">Currently, there is no option to override this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="08529-344">Parquet biçimi</span><span class="sxs-lookup"><span data-stu-id="08529-344">Parquet format</span></span>
<span data-ttu-id="08529-345">Parquet dosyalarını ayrıştırmak veya verileri Parquet biçiminde yazmak istiyorsanız `format` `type` özelliğini **ParquetFormat** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="08529-345">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="08529-346">typeProperties bölümünün içindeki Format bölümünde herhangi bir özellik belirtmenize gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="08529-346">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="08529-347">Örnek:</span><span class="sxs-lookup"><span data-stu-id="08529-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="08529-348">Şirket içi ve bulut veri depoları arasında Parquet dosyalarını **olduğu gibi** kopyalamıyorsanız, ağ geçidi cihazınıza JRE 8 (Java Çalışma Zamanı Ortamı) yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="08529-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="08529-349">64 bit ağ geçidi için 64 bit JRE, 32 bit ağ geçidi için de 32 bit JRE gerekir.</span><span class="sxs-lookup"><span data-stu-id="08529-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="08529-350">İki sürüme de [buradan](http://go.microsoft.com/fwlink/?LinkId=808605) ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="08529-351">Cihazınıza uygun olanı seçin.</span><span class="sxs-lookup"><span data-stu-id="08529-351">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="08529-352">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="08529-352">Note the following points:</span></span>

* <span data-ttu-id="08529-353">Karmaşık veri türleri desteklenmez (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="08529-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="08529-354">Parquet dosyası sıkıştırmayla ilgili şu seçeneklere sahiptir: NONE, SNAPPY, GZIP ve LZO.</span><span class="sxs-lookup"><span data-stu-id="08529-354">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="08529-355">Data Factory, bu sıkıştırma biçimlerinin herhangi birine sahip ORC dosyalarını okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="08529-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="08529-356">Verileri okumak için meta verilerdeki sıkıştırma kodlayıcısı/kod çözücüsünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="08529-356">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="08529-357">Ancak Data Factory bir Parquet dosyasına yazarken varsayılan Parquet biçimi SNAPPY seçeneğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="08529-357">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="08529-358">Şu anda bu davranışı geçersiz kılma seçeneği yoktur.</span><span class="sxs-lookup"><span data-stu-id="08529-358">Currently, there is no option to override this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="08529-359">Sıkıştırma desteği</span><span class="sxs-lookup"><span data-stu-id="08529-359">Compression support</span></span>
<span data-ttu-id="08529-360">Büyük veri kümeleri işleme g/ç ve ağ performans sorunlarına neden.</span><span class="sxs-lookup"><span data-stu-id="08529-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="08529-361">Bu nedenle, sıkıştırılmış veri depolarında yalnızca ağ üzerinden veri aktarımı hızlandırmak ve disk alanından tasarruf, ancak ayrıca büyük veri işlerken önemli performans geliştirmeleri getirin.</span><span class="sxs-lookup"><span data-stu-id="08529-361">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="08529-362">Şu anda sıkıştırma, Azure Blob veya şirket içi dosya sistemi gibi dosya tabanlı veri depoları için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="08529-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="08529-363">Bir veri kümesi sıkıştırma belirtmek için kullanın **sıkıştırma** aşağıdaki örnekteki gibi JSON veri kümesi özelliğinde:</span><span class="sxs-lookup"><span data-stu-id="08529-363">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

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

<span data-ttu-id="08529-364">Örnek veri kümesi kopyalama etkinliği çıkış olarak kullanılan varsayalım kopyalama etkinliği ile en iyi oranını kullanarak GZIP codec çıktı verilerini sıkıştırır ve Azure Blob Depolama pagecounts.csv.gz adlı bir dosyaya sıkıştırılmış veri yazma.</span><span class="sxs-lookup"><span data-stu-id="08529-364">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="08529-365">Veri sıkıştırma ayarları desteklenmez **AvroFormat**, **OrcFormat**, veya **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="08529-365">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="08529-366">Bu biçimler dosyalarında okurken, veri fabrikası algılar ve sıkıştırma codec meta verilerde kullanır.</span><span class="sxs-lookup"><span data-stu-id="08529-366">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="08529-367">Bu biçimler dosyalarında yazarken, veri fabrikası bu biçimi için varsayılan sıkıştırma codec seçer.</span><span class="sxs-lookup"><span data-stu-id="08529-367">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="08529-368">Örneğin, ZLIB OrcFormat ve ParquetFormat SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="08529-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="08529-369">**Sıkıştırma** bölüm iki özellik vardır:</span><span class="sxs-lookup"><span data-stu-id="08529-369">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="08529-370">**Tür:** olabilir sıkıştırma codec **GZIP**, **Deflate**, **bzıp2**, veya **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="08529-370">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="08529-371">**Düzeyi:** olabilir sıkıştırma oranı **Optimal** veya **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="08529-371">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="08529-372">**Hızlı:** sonuç dosyası en iyi şekilde sıkıştırılmaz olsa bile sıkıştırma işlemi mümkün olan en kısa sürede tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08529-372">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="08529-373">**En iyi**: işlemin tamamlanması çok uzun sürüyor olsa bile sıkıştırma işlemi en iyi şekilde, sıkıştırılmış.</span><span class="sxs-lookup"><span data-stu-id="08529-373">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="08529-374">Daha fazla bilgi için bkz: [sıkıştırma düzeyi](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="08529-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="08529-375">Belirttiğinizde `compression` bir girdi veri kümesi JSON özelliğinde, ardışık düzen sıkıştırılmış veri kaynağından; okuyabilir ve bir çıkış dataset JSON özelliğini belirttiğinizde kopyalama etkinliği hedefe sıkıştırılmış veri yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08529-375">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="08529-376">Bazı örnek senaryolar verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="08529-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="08529-377">Bir Azure blob okuma GZIP sıkıştırılmış verileri iptal ve sonuçta elde edilen veri bir Azure SQL veritabanına yazma.</span><span class="sxs-lookup"><span data-stu-id="08529-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="08529-378">Giriş Azure Blob kümesiyle tanımladığınız `compression` `type` JSON özellik GZIP olarak.</span><span class="sxs-lookup"><span data-stu-id="08529-378">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="08529-379">Şirket içi dosya sistemi düz metin dosyasından veri okunamıyor, GZip biçimi kullanarak Sıkıştır ve sıkıştırılmış verileri bir Azure blob yazma.</span><span class="sxs-lookup"><span data-stu-id="08529-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="08529-380">Bir çıktı Azure Blob kümesiyle tanımladığınız `compression` `type` JSON özellik GZip olarak.</span><span class="sxs-lookup"><span data-stu-id="08529-380">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="08529-381">FTP sunucusundan .zip dosyasını oku içindeki dosyaları alın ve bu dosyaların Azure Data Lake Store güden açın.</span><span class="sxs-lookup"><span data-stu-id="08529-381">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="08529-382">Bir giriş FTP kümesiyle tanımladığınız `compression` `type` JSON özelliği ZipDeflate olarak.</span><span class="sxs-lookup"><span data-stu-id="08529-382">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="08529-383">GZIP sıkıştırılmış verileri Azure blob'tan okuyun, iptal, bzıp2 kullanarak Sıkıştır ve bir Azure blob sonuç verileri yazma.</span><span class="sxs-lookup"><span data-stu-id="08529-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="08529-384">Giriş Azure Blob kümesiyle tanımladığınız `compression` `type` GZIP ve çıktı veri kümesi ile ayarlanan `compression` `type` bzıp2 için bu durumda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="08529-384">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="08529-385">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08529-385">Next steps</span></span>
<span data-ttu-id="08529-386">Azure Data Factory ile desteklenen dosya tabanlı veri depoları için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="08529-386">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="08529-387">Azure Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="08529-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="08529-388">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="08529-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="08529-389">FTP</span><span class="sxs-lookup"><span data-stu-id="08529-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="08529-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="08529-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="08529-391">Dosya Sistemi</span><span class="sxs-lookup"><span data-stu-id="08529-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="08529-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="08529-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
