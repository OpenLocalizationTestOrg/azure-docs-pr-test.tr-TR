## <a name="specifying-formats"></a><span data-ttu-id="6377e-101">Biçim belirtme</span><span class="sxs-lookup"><span data-stu-id="6377e-101">Specifying formats</span></span>
<span data-ttu-id="6377e-102">Azure Data Factory hello şu biçimi türlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="6377e-102">Azure Data Factory supports hello following format types:</span></span>

* [<span data-ttu-id="6377e-103">Metin Biçimi</span><span class="sxs-lookup"><span data-stu-id="6377e-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="6377e-104">JSON Biçimi</span><span class="sxs-lookup"><span data-stu-id="6377e-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="6377e-105">Avro Biçimi</span><span class="sxs-lookup"><span data-stu-id="6377e-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="6377e-106">ORC Biçimi</span><span class="sxs-lookup"><span data-stu-id="6377e-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="6377e-107">Parquet Biçimi</span><span class="sxs-lookup"><span data-stu-id="6377e-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="6377e-108">TextFormat belirtme</span><span class="sxs-lookup"><span data-stu-id="6377e-108">Specifying TextFormat</span></span>
<span data-ttu-id="6377e-109">Merhaba, tooparse hello metin dosyaları veya metin biçiminde hello veri yazmak istiyorsanız ayarlayın `format` `type` özelliği çok**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="6377e-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="6377e-110">Merhaba aşağıdakileri de belirtebilirsiniz **isteğe bağlı** hello özelliklerinde `format` bölümü.</span><span class="sxs-lookup"><span data-stu-id="6377e-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="6377e-111">Bkz: [TextFormat örnek](#textformat-example) nasıl bölüm tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="6377e-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="6377e-112">Özellik</span><span class="sxs-lookup"><span data-stu-id="6377e-112">Property</span></span> | <span data-ttu-id="6377e-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6377e-113">Description</span></span> | <span data-ttu-id="6377e-114">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="6377e-114">Allowed values</span></span> | <span data-ttu-id="6377e-115">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6377e-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6377e-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="6377e-116">columnDelimiter</span></span> |<span data-ttu-id="6377e-117">Merhaba karakter tooseparate sütunları bir dosyada kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6377e-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="6377e-118">Verilerinizi değil olasılıkla var olan nadir bir yazdırılamayan char toouse düşünebilirsiniz: Örneğin "Başlat, başlık (SOH) temsil eden \u0001" belirtin.</span><span class="sxs-lookup"><span data-stu-id="6377e-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="6377e-119">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6377e-119">Only one character is allowed.</span></span> <span data-ttu-id="6377e-120">Merhaba **varsayılan** değer **virgül (',')**.</span><span class="sxs-lookup"><span data-stu-id="6377e-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="6377e-121">toouse bir Unicode karakter başvurmak çok[Unicode karakterler](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello ilgili kod için.</span><span class="sxs-lookup"><span data-stu-id="6377e-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="6377e-122">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-122">No</span></span> |
| <span data-ttu-id="6377e-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="6377e-123">rowDelimiter</span></span> |<span data-ttu-id="6377e-124">Merhaba karakter tooseparate satır bir dosyada kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6377e-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="6377e-125">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6377e-125">Only one character is allowed.</span></span> <span data-ttu-id="6377e-126">Merhaba **varsayılan** değerdir herhangi biri üzerinde okuma değerleri aşağıdaki hello: **["\r\n", "\r", "\n"]** ve **"\r\n"** yazma üzerinde.</span><span class="sxs-lookup"><span data-stu-id="6377e-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="6377e-127">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-127">No</span></span> |
| <span data-ttu-id="6377e-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="6377e-128">escapeChar</span></span> |<span data-ttu-id="6377e-129">Merhaba özel karakter tooescape bir sütun ayırıcısı giriş dosyası hello içeriğinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6377e-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="6377e-130">Bir tablo için hem escapeChar hem de quoteChar parametrelerini aynı anda belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="6377e-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="6377e-131">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6377e-131">Only one character is allowed.</span></span> <span data-ttu-id="6377e-132">Varsayılan değer yoktur.</span><span class="sxs-lookup"><span data-stu-id="6377e-132">No default value.</span></span> <br/><br/><span data-ttu-id="6377e-133">Örnek: virgül varsa (', ') hello sütun sınırlayıcı ancak toohave hello virgül karakteri hello metin istediğiniz şekilde (örnek: "Hello, world"), '$' hello kaçış karakteri olarak tanımlamak ve dizesi kullanın "$Hello, world" Merhaba kaynağındaki.</span><span class="sxs-lookup"><span data-stu-id="6377e-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="6377e-134">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-134">No</span></span> |
| <span data-ttu-id="6377e-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="6377e-135">quoteChar</span></span> |<span data-ttu-id="6377e-136">Merhaba karakter tooquote bir dize değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6377e-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="6377e-137">Hello sütun ve satır sınırlayıcıları hello tırnak karakterleri içine hello dize değeri bir parçası olarak değerlendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="6377e-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="6377e-138">Bu özellik geçerli tooboth girdidir ve çıkış veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="6377e-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="6377e-139">Bir tablo için hem escapeChar hem de quoteChar parametrelerini aynı anda belirtemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="6377e-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="6377e-140">Yalnızca bir karaktere izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6377e-140">Only one character is allowed.</span></span> <span data-ttu-id="6377e-141">Varsayılan değer yoktur.</span><span class="sxs-lookup"><span data-stu-id="6377e-141">No default value.</span></span> <br/><br/><span data-ttu-id="6377e-142">Virgül varsa, örneğin, (', ') hello sütun sınırlayıcı ancak toohave virgül karakteri hello metin istediğiniz gibi (örnek: < Hello, world >), tanımlayabileceğiniz "(tırnak) tırnak işareti karakteri hello ve hello dizesini kullanın"Hello, world"Merhaba kaynağındaki.</span><span class="sxs-lookup"><span data-stu-id="6377e-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="6377e-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-143">No</span></span> |
| <span data-ttu-id="6377e-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="6377e-144">nullValue</span></span> |<span data-ttu-id="6377e-145">Bir veya daha fazla karakter toorepresent bir null değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6377e-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="6377e-146">Bir veya daha fazla karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="6377e-146">One or more characters.</span></span> <span data-ttu-id="6377e-147">Merhaba **varsayılan** değerler **"\N" ve "NULL"** okunur ve **"\N"** yazma üzerinde.</span><span class="sxs-lookup"><span data-stu-id="6377e-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="6377e-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-148">No</span></span> |
| <span data-ttu-id="6377e-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="6377e-149">encodingName</span></span> |<span data-ttu-id="6377e-150">Merhaba kodlama adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="6377e-150">Specify hello encoding name.</span></span> |<span data-ttu-id="6377e-151">Geçerli bir kodlama adı.</span><span class="sxs-lookup"><span data-stu-id="6377e-151">A valid encoding name.</span></span> <span data-ttu-id="6377e-152">Bkz. [Encoding.EncodingName Özelliği](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="6377e-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="6377e-153">Örnek: windows-1250 veya shift_jis.</span><span class="sxs-lookup"><span data-stu-id="6377e-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="6377e-154">Merhaba **varsayılan** değer **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="6377e-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="6377e-155">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-155">No</span></span> |
| <span data-ttu-id="6377e-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="6377e-156">firstRowAsHeader</span></span> |<span data-ttu-id="6377e-157">Tooconsider ilk satır bir başlık olarak hello olup olmadığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="6377e-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="6377e-158">Giriş veri kümesinde Data Factory ilk satırı üst bilgi olarak okur.</span><span class="sxs-lookup"><span data-stu-id="6377e-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="6377e-159">Çıkış veri kümesinde Data Factory ilk satırı üst bilgi olarak yazar.</span><span class="sxs-lookup"><span data-stu-id="6377e-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="6377e-160">Örnek senaryolar için bkz. [`firstRowAsHeader` ve `skipLineCount` kullanım senaryoları](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="6377e-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="6377e-161">True</span><span class="sxs-lookup"><span data-stu-id="6377e-161">True</span></span><br/><span data-ttu-id="6377e-162">**False (varsayılan)**</span><span class="sxs-lookup"><span data-stu-id="6377e-162">**False (default)**</span></span> |<span data-ttu-id="6377e-163">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-163">No</span></span> |
| <span data-ttu-id="6377e-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="6377e-164">skipLineCount</span></span> |<span data-ttu-id="6377e-165">Giriş dosyaları veri okuma satırları tooskip Hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6377e-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="6377e-166">SkipLineCount ve firstRowAsHeader belirtilirse, hello satırlar ilk atlanır ve hello üst bilgileri hello giriş dosyasından sonra okuyun.</span><span class="sxs-lookup"><span data-stu-id="6377e-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="6377e-167">Örnek senaryolar için bkz. [`firstRowAsHeader` ve `skipLineCount` kullanım senaryoları](#scenarios-for-using-firstrowasheader-and-skiplinecount).</span><span class="sxs-lookup"><span data-stu-id="6377e-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="6377e-168">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="6377e-168">Integer</span></span> |<span data-ttu-id="6377e-169">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-169">No</span></span> |
| <span data-ttu-id="6377e-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="6377e-170">treatEmptyAsNull</span></span> |<span data-ttu-id="6377e-171">Bir null olarak tootreat null veya boş dize değeri olup olmadığını belirten bir giriş dosyasından veri okuma.</span><span class="sxs-lookup"><span data-stu-id="6377e-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="6377e-172">**True (varsayılan)**</span><span class="sxs-lookup"><span data-stu-id="6377e-172">**True (default)**</span></span><br/><span data-ttu-id="6377e-173">False</span><span class="sxs-lookup"><span data-stu-id="6377e-173">False</span></span> |<span data-ttu-id="6377e-174">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="6377e-175">TextFormat örneği</span><span class="sxs-lookup"><span data-stu-id="6377e-175">TextFormat example</span></span>
<span data-ttu-id="6377e-176">Merhaba aşağıdaki örnek hello biçimi özelliklerinden bazıları için TextFormat gösterir.</span><span class="sxs-lookup"><span data-stu-id="6377e-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

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

<span data-ttu-id="6377e-177">toouse bir `escapeChar` yerine `quoteChar`, hello satırla değiştirin `quoteChar` escapeChar aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="6377e-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="6377e-178">firstRowAsHeader ve skipLineCount kullanım senaryoları</span><span class="sxs-lookup"><span data-stu-id="6377e-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="6377e-179">Dosya olmayan kaynak tooa metin dosyasından kopyalama ve tooadd hello şema meta verileri içeren bir başlık satırı istiyor musunuz (örneğin: SQL Şeması).</span><span class="sxs-lookup"><span data-stu-id="6377e-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="6377e-180">Belirtin `firstRowAsHeader` hello çıkış DataSet Bu senaryo için true.</span><span class="sxs-lookup"><span data-stu-id="6377e-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="6377e-181">Bir üst bilgi satırı tooa dosya olmayan havuz içeren bir metin dosyasından kopyalama ve satır toodrop istersiniz.</span><span class="sxs-lookup"><span data-stu-id="6377e-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="6377e-182">Belirtin `firstRowAsHeader` hello girdi veri kümesi olarak true.</span><span class="sxs-lookup"><span data-stu-id="6377e-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="6377e-183">Bir metin dosyasından kopyalama ve hiçbir veri veya üstbilgi bilgileri içeren birkaç satır hello başında tooskip istiyor.</span><span class="sxs-lookup"><span data-stu-id="6377e-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="6377e-184">Belirtin `skipLineCount` tooindicate hello satırları toobe sayısı atlandı.</span><span class="sxs-lookup"><span data-stu-id="6377e-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="6377e-185">Merhaba rest hello dosyasının bir başlık satırı içeriyorsa, ayrıca belirtebilirsiniz `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="6377e-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="6377e-186">Her iki `skipLineCount` ve `firstRowAsHeader` belirtilirse, hello satırları ilk atlanır ve hello üstbilgi bilgileri hello giriş dosyasından sonra okuyun</span><span class="sxs-lookup"><span data-stu-id="6377e-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="6377e-187">JsonFormat belirtme</span><span class="sxs-lookup"><span data-stu-id="6377e-187">Specifying JsonFormat</span></span>
<span data-ttu-id="6377e-188">çok**içeri/dışarı aktarma olarak JSON dosyaları-olduğu içine/Azure Cosmos DB'den**, bkz: [içeri/dışarı aktarma JSON belgeleri](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) hello Azure Cosmos DB bağlayıcı ayrıntılarla bölümünde.</span><span class="sxs-lookup"><span data-stu-id="6377e-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="6377e-189">Merhaba, tooparse hello JSON dosyaları veya JSON biçiminde hello veri yazmak istiyorsanız ayarlayın `format` `type` özelliği çok**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="6377e-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="6377e-190">Merhaba aşağıdakileri de belirtebilirsiniz **isteğe bağlı** hello özelliklerinde `format` bölümü.</span><span class="sxs-lookup"><span data-stu-id="6377e-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="6377e-191">Bkz: [JsonFormat örnek](#jsonformat-example) nasıl bölüm tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="6377e-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="6377e-192">Özellik</span><span class="sxs-lookup"><span data-stu-id="6377e-192">Property</span></span> | <span data-ttu-id="6377e-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6377e-193">Description</span></span> | <span data-ttu-id="6377e-194">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6377e-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6377e-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="6377e-195">filePattern</span></span> |<span data-ttu-id="6377e-196">Her JSON dosyasında depolanan verilerin Hello desen belirtin.</span><span class="sxs-lookup"><span data-stu-id="6377e-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="6377e-197">İzin verilen değerler: **setOfObjects** ve **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="6377e-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="6377e-198">Merhaba **varsayılan** değer **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="6377e-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="6377e-199">Bu desenler hakkında ayrıntılı bilgi için bkz. [JSON dosyası desenleri](#json-file-patterns).</span><span class="sxs-lookup"><span data-stu-id="6377e-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="6377e-200">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-200">No</span></span> |
| <span data-ttu-id="6377e-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="6377e-201">jsonNodeReference</span></span> | <span data-ttu-id="6377e-202">Bir dizinin içindeki hello nesnelerinden verileri ayıklamak ve tooiterate isterseniz hello ile aynı alan desen, bu dizinin hello JSON yolu belirtin.</span><span class="sxs-lookup"><span data-stu-id="6377e-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="6377e-203">Bu özellik yalnızca JSON dosyalarından veri kopyalarken desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6377e-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="6377e-204">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-204">No</span></span> |
| <span data-ttu-id="6377e-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="6377e-205">jsonPathDefinition</span></span> | <span data-ttu-id="6377e-206">Merhaba JSON yol ifadesi her sütun eşlemesi için özelleştirilmiş sütun adıyla (küçük başlayın) belirtin.</span><span class="sxs-lookup"><span data-stu-id="6377e-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="6377e-207">Bu özellik yalnızca JSON dosyalarından veri kopyalarken desteklenir. Verileri nesne veya diziden ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6377e-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="6377e-208">Kök nesnede altında alanlar için kök $ ile Başlat; tarafından seçilen hello dizinin içindeki alanlar için `jsonNodeReference` özelliği, hello dizi öğesinin başından.</span><span class="sxs-lookup"><span data-stu-id="6377e-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="6377e-209">Bkz: [JsonFormat örnek](#jsonformat-example) nasıl bölüm tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="6377e-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="6377e-210">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-210">No</span></span> |
| <span data-ttu-id="6377e-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="6377e-211">encodingName</span></span> |<span data-ttu-id="6377e-212">Merhaba kodlama adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="6377e-212">Specify hello encoding name.</span></span> <span data-ttu-id="6377e-213">Geçerli kodlama adlar Hello listesi için bkz: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) özelliği.</span><span class="sxs-lookup"><span data-stu-id="6377e-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="6377e-214">Örneğin: windows-1250 veya shift_jis.</span><span class="sxs-lookup"><span data-stu-id="6377e-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="6377e-215">Merhaba **varsayılan** değer: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="6377e-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="6377e-216">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-216">No</span></span> |
| <span data-ttu-id="6377e-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="6377e-217">nestingSeparator</span></span> |<span data-ttu-id="6377e-218">Kullanılan tooseparate iç içe geçme düzeyi karakter.</span><span class="sxs-lookup"><span data-stu-id="6377e-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="6377e-219">Merhaba varsayılan değer '.' (nokta).</span><span class="sxs-lookup"><span data-stu-id="6377e-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="6377e-220">Hayır</span><span class="sxs-lookup"><span data-stu-id="6377e-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="6377e-221">JSON dosyası desenleri</span><span class="sxs-lookup"><span data-stu-id="6377e-221">JSON file patterns</span></span>

<span data-ttu-id="6377e-222">Kopyalama etkinliği, JSON dosyalarının şu desenlerini ayrıştırabilir:</span><span class="sxs-lookup"><span data-stu-id="6377e-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="6377e-223">**1. Tür: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="6377e-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="6377e-224">Her dosya tek bir nesne veya satırlara ayrılmış/bitiştirilmiş birden fazla nesne içerir.</span><span class="sxs-lookup"><span data-stu-id="6377e-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="6377e-225">Bu seçenek bir çıkış veri kümesinde belirlendiğinde, kopyalama etkinliği her satırda bir nesnenin bulunduğu (satırlara ayrılmış) tek bir JSON dosyası üretir.</span><span class="sxs-lookup"><span data-stu-id="6377e-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="6377e-226">**tek nesne JSON örneği**</span><span class="sxs-lookup"><span data-stu-id="6377e-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="6377e-227">**satırlara ayrılmış JSON örneği**</span><span class="sxs-lookup"><span data-stu-id="6377e-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="6377e-228">**bitiştirilmiş JSON örneği**</span><span class="sxs-lookup"><span data-stu-id="6377e-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="6377e-229">**2. Tür: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="6377e-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="6377e-230">Her dosya bir nesne dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="6377e-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="6377e-231">JsonFormat örneği</span><span class="sxs-lookup"><span data-stu-id="6377e-231">JsonFormat example</span></span>

<span data-ttu-id="6377e-232">**Örnek Durum 1: JSON dosyalarından veri kopyalama**</span><span class="sxs-lookup"><span data-stu-id="6377e-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="6377e-233">İki tür örnekleri verileri JSON dosyaları kopyalarken görebilir ve genel noktaları toonote hello:</span><span class="sxs-lookup"><span data-stu-id="6377e-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="6377e-234">**Örnek 1: nesne ve diziden veri ayıklama**</span><span class="sxs-lookup"><span data-stu-id="6377e-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="6377e-235">Bu örnekte, bir kök JSON nesnesi toosingle kaydı tablo sonuç eşler bekler.</span><span class="sxs-lookup"><span data-stu-id="6377e-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="6377e-236">İçeriği aşağıdaki hello ile bir JSON dosyası varsa:</span><span class="sxs-lookup"><span data-stu-id="6377e-236">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="6377e-237">ve bunu bir Azure SQL tablosuna hello aşağıdaki biçimi, veri nesneleri hem dizi çıkartarak toocopy istiyor:</span><span class="sxs-lookup"><span data-stu-id="6377e-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="6377e-238">id</span><span class="sxs-lookup"><span data-stu-id="6377e-238">id</span></span> | <span data-ttu-id="6377e-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="6377e-239">deviceType</span></span> | <span data-ttu-id="6377e-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="6377e-240">targetResourceType</span></span> | <span data-ttu-id="6377e-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="6377e-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="6377e-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="6377e-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6377e-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="6377e-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="6377e-244">PC</span><span class="sxs-lookup"><span data-stu-id="6377e-244">PC</span></span> | <span data-ttu-id="6377e-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="6377e-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="6377e-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="6377e-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="6377e-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="6377e-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="6377e-248">Merhaba girdi veri kümesi ile **JsonFormat** türü şu şekilde tanımlanır: (yalnızca hello ilgili bölümleri kısmi tanımıyla).</span><span class="sxs-lookup"><span data-stu-id="6377e-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="6377e-249">Daha ayrıntılı belirtmek gerekirse:</span><span class="sxs-lookup"><span data-stu-id="6377e-249">More specifically:</span></span>

- <span data-ttu-id="6377e-250">`structure`Bölüm tootabular veri dönüştürülürken özelleştirilmiş hello sütun adları ve hello karşılık gelen veri türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6377e-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="6377e-251">Bu bölüm **isteğe bağlı** toodo sütun eşlemesi gerekmedikçe.</span><span class="sxs-lookup"><span data-stu-id="6377e-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="6377e-252">Ayrıntılı bilgi için bkz. [Dikdörtgen veri kümeleri için yapı tanımını belirtme](#specifying-structure-definition-for-rectangular-datasets).</span><span class="sxs-lookup"><span data-stu-id="6377e-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="6377e-253">`jsonPathDefinition`Burada tooextract hello verilerden belirten her sütun için Hello JSON yolu belirtir.</span><span class="sxs-lookup"><span data-stu-id="6377e-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="6377e-254">kullanabileceğiniz toocopy veri dizisinden **array [x] .property** özelliği hello un x. nesne veya size verilen hello tooextract değerini kullanabilir  **dizisi [*] .property** toofind Böyle bir özellik içeren herhangi bir nesneden Hello değeri.</span><span class="sxs-lookup"><span data-stu-id="6377e-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="6377e-255">**Örnek 2: çapraz hello aynı diziden desen ile birden çok nesne uygulayın.**</span><span class="sxs-lookup"><span data-stu-id="6377e-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="6377e-256">Bu örnekte, tablo sonuç içinde birden çok kayıt içine tootransform bir kök JSON nesnesi bekler.</span><span class="sxs-lookup"><span data-stu-id="6377e-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="6377e-257">İçeriği aşağıdaki hello ile bir JSON dosyası varsa:</span><span class="sxs-lookup"><span data-stu-id="6377e-257">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="6377e-258">ve bunu bir Azure SQL tablosuna hello aşağıdaki biçiminde hello veri hello dizinin içindeki düzleştirme tarafından toocopy istediğiniz ve çapraz birleştirme hello ortak kök bilgileri ile:</span><span class="sxs-lookup"><span data-stu-id="6377e-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="6377e-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="6377e-259">ordernumber</span></span> | <span data-ttu-id="6377e-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="6377e-260">orderdate</span></span> | <span data-ttu-id="6377e-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="6377e-261">order_pd</span></span> | <span data-ttu-id="6377e-262">order_price</span><span class="sxs-lookup"><span data-stu-id="6377e-262">order_price</span></span> | <span data-ttu-id="6377e-263">city</span><span class="sxs-lookup"><span data-stu-id="6377e-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6377e-264">01</span><span class="sxs-lookup"><span data-stu-id="6377e-264">01</span></span> | <span data-ttu-id="6377e-265">20170122</span><span class="sxs-lookup"><span data-stu-id="6377e-265">20170122</span></span> | <span data-ttu-id="6377e-266">P1</span><span class="sxs-lookup"><span data-stu-id="6377e-266">P1</span></span> | <span data-ttu-id="6377e-267">23</span><span class="sxs-lookup"><span data-stu-id="6377e-267">23</span></span> | <span data-ttu-id="6377e-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="6377e-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="6377e-269">01</span><span class="sxs-lookup"><span data-stu-id="6377e-269">01</span></span> | <span data-ttu-id="6377e-270">20170122</span><span class="sxs-lookup"><span data-stu-id="6377e-270">20170122</span></span> | <span data-ttu-id="6377e-271">P2</span><span class="sxs-lookup"><span data-stu-id="6377e-271">P2</span></span> | <span data-ttu-id="6377e-272">13</span><span class="sxs-lookup"><span data-stu-id="6377e-272">13</span></span> | <span data-ttu-id="6377e-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="6377e-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="6377e-274">01</span><span class="sxs-lookup"><span data-stu-id="6377e-274">01</span></span> | <span data-ttu-id="6377e-275">20170122</span><span class="sxs-lookup"><span data-stu-id="6377e-275">20170122</span></span> | <span data-ttu-id="6377e-276">P3</span><span class="sxs-lookup"><span data-stu-id="6377e-276">P3</span></span> | <span data-ttu-id="6377e-277">231</span><span class="sxs-lookup"><span data-stu-id="6377e-277">231</span></span> | <span data-ttu-id="6377e-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="6377e-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="6377e-279">Merhaba girdi veri kümesi ile **JsonFormat** türü şu şekilde tanımlanır: (yalnızca hello ilgili bölümleri kısmi tanımıyla).</span><span class="sxs-lookup"><span data-stu-id="6377e-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="6377e-280">Daha ayrıntılı belirtmek gerekirse:</span><span class="sxs-lookup"><span data-stu-id="6377e-280">More specifically:</span></span>

- <span data-ttu-id="6377e-281">`structure`Bölüm tootabular veri dönüştürülürken özelleştirilmiş hello sütun adları ve hello karşılık gelen veri türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6377e-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="6377e-282">Bu bölüm **isteğe bağlı** toodo sütun eşlemesi gerekmedikçe.</span><span class="sxs-lookup"><span data-stu-id="6377e-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="6377e-283">Ayrıntılı bilgi için bkz. [Dikdörtgen veri kümeleri için yapı tanımını belirtme](#specifying-structure-definition-for-rectangular-datasets).</span><span class="sxs-lookup"><span data-stu-id="6377e-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="6377e-284">`jsonNodeReference`aynı desen altında hello hello nesneleriyle tooiterate ve ayıklama verilerini gösteren **dizi** orderlines.</span><span class="sxs-lookup"><span data-stu-id="6377e-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="6377e-285">`jsonPathDefinition`Burada tooextract hello verilerden belirten her sütun için Hello JSON yolu belirtir.</span><span class="sxs-lookup"><span data-stu-id="6377e-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="6377e-286">Bu örnekte "$.", "order_pd" ve "order_price" "$" olmadan hello array öğesinden türetilen yoluyla tanımlı başlangıç JSON yolu ile kök nesnesi altında "ordernumber", "orderdate" ve "Şehir" olur.</span><span class="sxs-lookup"><span data-stu-id="6377e-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="6377e-287">**Hello aşağıdaki noktaları göz önünde bulundurun:**</span><span class="sxs-lookup"><span data-stu-id="6377e-287">**Note hello following points:**</span></span>

* <span data-ttu-id="6377e-288">Merhaba, `structure` ve `jsonPathDefinition` hello Data Factory veri kümesi içinde hello tanımlanmayan kopyalama etkinliği hello hello ilk nesne şemadan ve nesnenin tamamı hello düzleştirmek algılar.</span><span class="sxs-lookup"><span data-stu-id="6377e-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="6377e-289">Merhaba JSON girişi bir dizi varsa, varsayılan olarak hello kopyalama etkinliği hello tüm dizi değeri bir dizeye dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="6377e-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="6377e-290">Tooextract verileri kullanarak ondan seçebilirsiniz `jsonNodeReference` ve/veya `jsonPathDefinition`, veya içinde belirterek değil atlayabilirsiniz `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="6377e-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="6377e-291">Varsa yinelenen adları, aynı düzeydeki Merhaba, hello kopyalama etkinliği hello sonuncu seçer.</span><span class="sxs-lookup"><span data-stu-id="6377e-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="6377e-292">Özellik adları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="6377e-292">Property names are case-sensitive.</span></span> <span data-ttu-id="6377e-293">Aynı ada ancak farklı büyük/küçük harf düzenine sahip iki özellik, iki ayrı özellik olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="6377e-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="6377e-294">**Durum 2: veri tooJSON dosyası yazılıyor**</span><span class="sxs-lookup"><span data-stu-id="6377e-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="6377e-295">SQL Veritabanında aşağıdaki gibi bir tabloya sahipseniz:</span><span class="sxs-lookup"><span data-stu-id="6377e-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="6377e-296">id</span><span class="sxs-lookup"><span data-stu-id="6377e-296">id</span></span> | <span data-ttu-id="6377e-297">order_date</span><span class="sxs-lookup"><span data-stu-id="6377e-297">order_date</span></span> | <span data-ttu-id="6377e-298">order_price</span><span class="sxs-lookup"><span data-stu-id="6377e-298">order_price</span></span> | <span data-ttu-id="6377e-299">order_by</span><span class="sxs-lookup"><span data-stu-id="6377e-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6377e-300">1</span><span class="sxs-lookup"><span data-stu-id="6377e-300">1</span></span> | <span data-ttu-id="6377e-301">20170119</span><span class="sxs-lookup"><span data-stu-id="6377e-301">20170119</span></span> | <span data-ttu-id="6377e-302">2000</span><span class="sxs-lookup"><span data-stu-id="6377e-302">2000</span></span> | <span data-ttu-id="6377e-303">David</span><span class="sxs-lookup"><span data-stu-id="6377e-303">David</span></span> |
| <span data-ttu-id="6377e-304">2</span><span class="sxs-lookup"><span data-stu-id="6377e-304">2</span></span> | <span data-ttu-id="6377e-305">20170120</span><span class="sxs-lookup"><span data-stu-id="6377e-305">20170120</span></span> | <span data-ttu-id="6377e-306">3500</span><span class="sxs-lookup"><span data-stu-id="6377e-306">3500</span></span> | <span data-ttu-id="6377e-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="6377e-307">Patrick</span></span> |
| <span data-ttu-id="6377e-308">3</span><span class="sxs-lookup"><span data-stu-id="6377e-308">3</span></span> | <span data-ttu-id="6377e-309">20170121</span><span class="sxs-lookup"><span data-stu-id="6377e-309">20170121</span></span> | <span data-ttu-id="6377e-310">4000</span><span class="sxs-lookup"><span data-stu-id="6377e-310">4000</span></span> | <span data-ttu-id="6377e-311">Jason</span><span class="sxs-lookup"><span data-stu-id="6377e-311">Jason</span></span> |

<span data-ttu-id="6377e-312">ve toowrite tooa JSON nesnesinde biçimi altındaki beklediğiniz her kayıt için:</span><span class="sxs-lookup"><span data-stu-id="6377e-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
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

<span data-ttu-id="6377e-313">Merhaba çıkış veri kümesi ile **JsonFormat** türü şu şekilde tanımlanır: (yalnızca hello ilgili bölümleri kısmi tanımıyla).</span><span class="sxs-lookup"><span data-stu-id="6377e-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="6377e-314">Daha belirgin olarak `structure` bölüm hedef dosyasında özelleştirilmiş hello özellik adlarını tanımlar `nestingSeparator` (varsayılan değer ".") kullanılan tooidentify hello iç içe katman hello adından olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6377e-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="6377e-315">Bu bölüm **isteğe bağlı** toochange hello özellik adı kaynak sütun adı ile karşılaştırmak istediğiniz ya da hello özelliklerden bazıları iç içe sürece.</span><span class="sxs-lookup"><span data-stu-id="6377e-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="6377e-316">AvroFormat belirtme</span><span class="sxs-lookup"><span data-stu-id="6377e-316">Specifying AvroFormat</span></span>
<span data-ttu-id="6377e-317">Tooparse hello Avro dosyalarının istediğiniz veya Avro biçiminde hello veri yazmak istiyorsanız, hello ayarlayın `format` `type` özelliği çok**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="6377e-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="6377e-318">Merhaba typeProperties bölüm içindeki hello biçimi bölümünde herhangi bir özellik toospecify gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6377e-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="6377e-319">Örnek:</span><span class="sxs-lookup"><span data-stu-id="6377e-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="6377e-320">bir Hive tablosu toouse Avro biçimi, başvurabilirsiniz çok[Apache Hive'nın Öğreticisi](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="6377e-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="6377e-321">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="6377e-321">Note hello following points:</span></span>  

* <span data-ttu-id="6377e-322">[Karmaşık veri türleri](http://avro.apache.org/docs/current/spec.html#schema_complex) desteklenmez (kayıtlar, enum'lar, diziler, eşlemeler, birleşimler ve sabitler).</span><span class="sxs-lookup"><span data-stu-id="6377e-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="6377e-323">OrcFormat belirtme</span><span class="sxs-lookup"><span data-stu-id="6377e-323">Specifying OrcFormat</span></span>
<span data-ttu-id="6377e-324">Merhaba, tooparse hello ORC dosyaları veya ORC biçiminde hello veri yazmak istiyorsanız ayarlayın `format` `type` özelliği çok**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="6377e-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="6377e-325">Merhaba typeProperties bölüm içindeki hello biçimi bölümünde herhangi bir özellik toospecify gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6377e-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="6377e-326">Örnek:</span><span class="sxs-lookup"><span data-stu-id="6377e-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="6377e-327">ORC dosyaları kopyalıyorsanız değil, **olarak-olduğu** şirket içi ve bulut arasında veri depolarına, ağ geçidi makinenizde tooinstall hello JRE 8 (Java Çalışma zamanı ortamı) gerekir.</span><span class="sxs-lookup"><span data-stu-id="6377e-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="6377e-328">64 bit ağ geçidi için 64 bit JRE, 32 bit ağ geçidi için de 32 bit JRE gerekir.</span><span class="sxs-lookup"><span data-stu-id="6377e-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="6377e-329">İki sürüme de [buradan](http://go.microsoft.com/fwlink/?LinkId=808605) ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6377e-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="6377e-330">Merhaba uygun olanı seçin.</span><span class="sxs-lookup"><span data-stu-id="6377e-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="6377e-331">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="6377e-331">Note hello following points:</span></span>

* <span data-ttu-id="6377e-332">Karmaşık veri türleri desteklenmez (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="6377e-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="6377e-333">ORC dosyası [sıkıştırmayla ilgili üç seçeneğe sahiptir](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="6377e-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="6377e-334">Data Factory, bu sıkıştırma biçimlerinin herhangi birine sahip ORC dosyalarını okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="6377e-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="6377e-335">Merhaba sıkıştırma kullanır codec olduğu hello meta veri tooread hello verileri.</span><span class="sxs-lookup"><span data-stu-id="6377e-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="6377e-336">Ancak, tooan ORC dosyasına yazarken, veri fabrikası ZLIB, ORC için hello varsayılan olduğu seçer.</span><span class="sxs-lookup"><span data-stu-id="6377e-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="6377e-337">Şu anda bu davranış hiçbir seçeneği toooverride yoktur.</span><span class="sxs-lookup"><span data-stu-id="6377e-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="6377e-338">ParquetFormat belirtme</span><span class="sxs-lookup"><span data-stu-id="6377e-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="6377e-339">Tooparse hello Parquet dosyalarının istediğiniz veya Parquet biçiminde hello veri yazmak istiyorsanız, hello ayarlayın `format` `type` özelliği çok**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="6377e-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="6377e-340">Merhaba typeProperties bölüm içindeki hello biçimi bölümünde herhangi bir özellik toospecify gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6377e-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="6377e-341">Örnek:</span><span class="sxs-lookup"><span data-stu-id="6377e-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="6377e-342">Parquet dosyaları kopyalıyorsanız değil, **olarak-olduğu** şirket içi ve bulut arasında veri depolarına, ağ geçidi makinenizde tooinstall hello JRE 8 (Java Çalışma zamanı ortamı) gerekir.</span><span class="sxs-lookup"><span data-stu-id="6377e-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="6377e-343">64 bit ağ geçidi için 64 bit JRE, 32 bit ağ geçidi için de 32 bit JRE gerekir.</span><span class="sxs-lookup"><span data-stu-id="6377e-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="6377e-344">İki sürüme de [buradan](http://go.microsoft.com/fwlink/?LinkId=808605) ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6377e-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="6377e-345">Merhaba uygun olanı seçin.</span><span class="sxs-lookup"><span data-stu-id="6377e-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="6377e-346">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="6377e-346">Note hello following points:</span></span>

* <span data-ttu-id="6377e-347">Karmaşık veri türleri desteklenmez (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="6377e-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="6377e-348">Parquet dosya sıkıştırma ilgili seçenekleri aşağıdaki hello vardır: NONE, SNAPPY, GZIP ve LZO.</span><span class="sxs-lookup"><span data-stu-id="6377e-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="6377e-349">Data Factory, bu sıkıştırma biçimlerinin herhangi birine sahip ORC dosyalarını okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="6377e-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="6377e-350">Merhaba sıkıştırma codec hello meta veri tooread hello verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="6377e-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="6377e-351">Ancak, tooa Parquet dosyasına yazarken, veri fabrikası SNAPPY, Parquet biçiminde hello varsayılan olduğu seçer.</span><span class="sxs-lookup"><span data-stu-id="6377e-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="6377e-352">Şu anda bu davranış hiçbir seçeneği toooverride yoktur.</span><span class="sxs-lookup"><span data-stu-id="6377e-352">Currently, there is no option toooverride this behavior.</span></span>
