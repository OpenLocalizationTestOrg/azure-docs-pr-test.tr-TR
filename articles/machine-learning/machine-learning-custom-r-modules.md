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
# <a name="author-custom-r-modules-in-azure-machine-learning"></a>Azure Machine Learning'de özel R modülleri yazma
Bu konuda açıklanmaktadır nasıl tooauthor ve Azure Machine learning'de özel R modülü dağıtın. Özel R modülleri nelerdir ve hangi dosyaları kullanılan toodefine açıklar bunları. Nasıl tooconstruct hello bir modülün tanımlanması dosyaları ve nasıl tooregister hello Machine Learning çalışma alanındaki dağıtım için modülü gösterilmektedir. Merhaba öğeleri ve özniteliklerinin hello özel modülü hello tanımında kullanılan sonra daha ayrıntılı olarak açıklanmıştır. Nasıl toouse yardımcı işlevleri, dosya ve birden çok çıkış da ele alınmıştır. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a>Özel bir R Modülü nedir?
A **özel Modülü** olan olabilir kullanıcı tanımlı bir modül karşıya tooyour çalışma ve bir Azure Machine Learning deneme bir parçası olarak yürütülür. A **özel R Modülü** kullanıcı tanımlı bir R işlev yürüten özel bir modüldür. **R** istatistiksel bilgi işlem ve istatistikçiler ve veri bilimcilerine tarafından algoritmaları uygulamak için yaygın olarak kullanılan grafik için bir programlama dilidir. Şu anda R özel modüller, ancak destek ek dilleri zamanlandığı yönelik için gelecek sürümlerde desteklenen hello yalnızca bir dildir.

Özel modüller sahip **birinci sınıf durum** Azure Machine learning'de hello herkese açık bunlar diğer modülü gibi kullanılabilir. Yayımlanan denemeler veya görselleştirmeleri dahil, diğer modüllerle çalıştırılabilir. Hello modülü tarafından uygulanan hello algoritması üzerinde denetim sahibi, kullanılan giriş ve çıkış bağlantı noktaları toobe Merhaba, modelleme parametreleri ve diğer çeşitli çalışma zamanı davranışları hello. Özel modüller içeren bir deney, Cortana Intelligence Galerisi hello kolay paylaşımı için de yayımlanabilir.

## <a name="files-in-a-custom-r-module"></a>Özel bir R Modülü dosyaları
Özel bir R modülü, en az iki dosyalarını içeren bir .zip dosyası tanımlanır:

* A **kaynak dosyası** hello modülü tarafından kullanıma sunulan hello R işlevi uygular
* Bir **XML tanım dosyasını** hello özel modülü arabirimi açıklanmaktadır

Ek yardımcı dosyalar da hello özel modülünden erişilebilir işlevselliği sağlayan hello .zip dosya eklenebilir. Bu seçenek hello ele alınmıştır **bağımsız değişkenleri** hello başvuru bölümünde parçası **hello XML tanım dosyasını öğelerinde** hello hızlı başlangıç örnek aşağıdaki.

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a>Hızlı Başlangıç örnek: tanımlamak, paket ve özel bir R modülü kaydetme
Bu örnek nasıl tooconstruct hello özel bir R modülü tarafından gerekli olan dosyaları gösterir, bunları bir zip dosyası ve ardından kayıt hello modülü Machine Learning çalışma alanınızdaki paketi. Merhaba örnek zip paketini ve örnek dosyaları yüklenebilir [CustomAddRows.zip karşıdan dosya](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).

## <a name="hello-source-file"></a>Merhaba kaynak dosyası
Hello örneği göz önünde bulundurun bir **özel Add Rows** hello hello standart uygulaması değiştirir Modülü **Add Rows** modülü kullanılan iki veri kümesi (veri çerçevelerini) tooconcatenate satırları (gözlemleri). Merhaba standart **Add Rows** modülü hello ikinci girdi veri kümesi toohello sonuna hello kullanarak hello ilk girdi veri kümesi hello satırlarını ekler `rbind` algoritması. özelleştirilmiş hello `CustomAddRows` işlevi benzer şekilde iki veri kümesi kabul eder, ancak ayrıca bir Boolean takas parametresi ek bir girdi olarak kabul eder. Merhaba takas parametresi çok ayarlarsanız**yanlış**, onu standart uygulama hello gibi hello aynı veri kümesi döndürür. Ancak hello takas parametresi ise **doğru**, hello işlevi hello ikinci veri kümesi ilk girdi veri kümesi toohello sonuna satır yerine ekler. Merhaba R hello uyarlamasını içeren hello CustomAddRows.R dosyası `CustomAddRows` hello tarafından kullanıma sunulan işlevi **özel Add Rows** modül R koddan hello sahiptir.

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

### <a name="hello-xml-definition-file"></a>Merhaba XML tanım dosyası
tooexpose bu `CustomAddRows` toospecify işlevi bir Azure Machine Learning modülü, bir XML tanım dosyası olarak oluşturulan nasıl hello **özel Add Rows** modülü görünüş ve davranışı aynıdır. 

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


Merhaba değerini hello kritik toonote olan **kimliği** hello özniteliklerini **giriş** ve **Arg** hello XML dosyasındaki öğeleri hello R hello işlevi parametre adları eşleşmelidir Merhaba CustomAddRows.R dosyasında tam olarak kod: (*dataset1*, *dataset2*, ve *takas* hello örnekte). Benzer şekilde, hello değerini hello **entryPoint** hello özniteliği **dil** öğesi eşleşmelidir hello R betiği hello işlevinde hello adı: (*CustomAddRows* Merhaba örnekte). 

Buna karşılık, hello **kimliği** özniteliği hello için **çıkış** öğesi hello R betiği tooany değişkenleri karşılık gelmiyor. Birden fazla çıkış gerekli olduğunda, bir liste yerleştirilen sonuçlarıyla hello R işlevinden yalnızca dönmek *hello de aynı sırada* olarak **çıkışları** öğeleri hello XML dosyasında bildirilen.

### <a name="package-and-register-hello-module"></a>Paket ve kayıt hello Modülü
Bu iki dosyaları olarak kaydetmeniz *CustomAddRows.R* ve *CustomAddRows.xml* ve ardından zip hello iki dosya birlikte içine bir *CustomAddRows.zip* dosya.

Merhaba, Machine Learning çalışma alanına gidin tooyour çalışma alanında hello Machine Learning Studio, bunları tıklatın tooregister **+ yeni** hello alta düğmesini tıklatın ve seçin **MODÜL ZIP PAKETİNİ gelen ->** tooupload Merhaba yeni **özel Add Rows** modülü.

![Zip karşıya yükle](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

Merhaba **özel Add Rows** modülüdür şimdi, Machine Learning denemelerini tarafından erişilen hazır toobe.

## <a name="elements-in-hello-xml-definition-file"></a>Merhaba XML tanım dosyasını öğeleri
### <a name="module-elements"></a>Modül öğeleri
Merhaba **Modülü** kullanılan toodefine hello XML dosyasında özel bir modülü bir öğedir. Birden fazla modülü birden çok kullanarak bir XML dosyasında tanımlanabilir **Modülü** öğeleri. Her modül çalışma alanınızda benzersiz bir ad olmalıdır. Özel bir modülü aynı var olan bir özel modül adı hello kaydetme ve hello ile yeni bir hello var olan bir modül değiştirir. Özel modüller ancak olabilir aynı adı var olan bir Azure Machine Learning modül hello kayıtlı. Bu nedenle, hello görünüyorsa **özel** hello modül paleti kategorisi.

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


Merhaba içinde **Modülü** öğesi, iki ek isteğe bağlı öğeleri belirtebilirsiniz:

* bir **sahibi** hello modüle katıştırılmış öğesi  
* bir **açıklama** hello modülü için hızlı Yardımı'nda görüntülenir ve hello Machine Learning UI hello modülünde üzerine getirdiğinizde metni içeren öğe.

Kuralları hello modülü öğelerinde karakter sınırları için:

* Merhaba hello değerini **adı** hello özniteliğinde **Modülü** öğesi uzunluğu 64 karakteri aşmamalıdır. 
* Merhaba Merhaba içeriğine **açıklama** öğesi 128 karakterden uzun olamaz.
* Merhaba Merhaba içeriğine **sahibi** öğesi 32 karakterden uzun olamaz.

Bir modülün sonuçları belirleyici olabilir veya nondeterministic.* * varsayılan olarak tüm modüllerin toobe belirleyici olarak kabul edilir. Diğer bir deyişle, değişmeyen dizi giriş parametreleri ve verileri verildiğinde, hello modülü aynı eacRAND veya bir functionh çalıştırıldığında sonuçları hello döndürmelidir. Bu davranış verildiğinde, Azure Machine Learning Studio, bir parametre değilse belirleyici olarak işaretlenmiş Modüller yalnızca yeniden çalıştırır veya hello giriş verileri değiştirildi. Merhaba önbelleğe alınan sonuçları döndüren çok daha hızlı denemeler yürütülmesini sağlar.

RAND veya hello geçerli tarih veya saat döndüren bir işlev gibi belirleyici işlevleri vardır. Modülünüzün belirleyici olmayan bir işlev kullanıyorsa, bu hello modül ayarı hello tarafından isteğe bağlı belirleyici belirtebilirsiniz **IsDeterministic** çok öznitelik**FALSE**. Bu, her hello deneme çalıştırdığınızda, hello modül girişi ve parametreleri değişip değişmediğini olsa bile bu hello modülü yeniden çalıştırılır oluşturmasını sağlar. 

### <a name="language-definition"></a>Dil tanımı
Merhaba **dil** XML tanım dosyasını öğedir kullanılan toospecify hello özel modülü dili. Şu anda, R hello yalnızca desteklenen dil değil. Merhaba hello değerini **sourceFile** özniteliği hello işlevi toocall hello modülü çalıştırdığınızda içeren hello R dosyasının hello adı olmalıdır. Bu dosya hello zip paketinin bir parçası olması gerekir. Merhaba hello değerini **entryPoint** özniteliği çağrılan hello işlevi hello adıdır ve hello kaynak dosyasında tanımlanmış geçerli bir işlev eşleşmesi gerekir.

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a>Bağlantı Noktaları
Merhaba özel bir modülü için giriş ve çıkış bağlantı noktalarını hello alt öğelerinde belirtilen **bağlantı noktalarını** hello XML tanım dosyasını bölümü. Bu öğelerin sırasını Hello hello düzeni deneyimli (UX) kullanıcılar tarafından belirler. Merhaba ilk alt **giriş** veya **çıkış** hello listelenen **bağlantı noktalarını** hello XML dosyasının öğesinin hello en sol giriş bağlantı noktası hello Machine Learning UX olur
Her giriş ve çıkış bağlantı noktasına isteğe sahip **açıklama** hello Machine Learning UI hello bağlantı noktası üzerinden hello fare imlecini getirdiğinizde gösterilen hello metin belirtir alt öğesi.

**Bağlantı noktası kuralları**:

* En fazla **giriş ve çıkış bağlantı noktaları** her biri için 8'dir.

### <a name="input-elements"></a>Giriş öğeleri
Giriş bağlantı noktaları toopass veri tooyour R işlevi ve çalışma izin verir. Merhaba **veri türleri** giriş bağlantı noktaları gibi için desteklenir: 

**DataTable:** bu tür tooyour R işlevi data.frame geçirilir. Aslında, Machine Learning ve, tarafından desteklenen tüm türleri (örneğin, CSV dosyalarını veya ARFF dosyaları) ile uyumlu **DataTable** dönüştürülmüş tooa data.frame otomatik olarak olursunuz. 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

Merhaba **kimliği** her ilişkilendirilmiş özniteliği **DataTable** giriş bağlantı noktası benzersiz bir değer olmalıdır ve bu değer, R işlevi parametresinde belirtilen ilgili eşleşmesi gerekir.
İsteğe bağlı **DataTable** Giriş bir deney olarak geçmedi bağlantı noktalarını hello değere sahip **NULL** geçirilen toohello R işlev ve isteğe bağlı zip bağlantı noktalarını hello giriş bağlı değilse yoksayılır. Merhaba **isteğe bağlıdır** özniteliktir hem hello için isteğe bağlı **DataTable** ve **Zip** türleri ve olduğu *false* varsayılan olarak.

**Zip:** özel modüller bir zip dosyası giriş olarak kabul edebilir. Bu giriş hello R çalışma dizinini işlevinizin açılmış

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

Özel R modülleri için bir Zip bağlantı noktası için hello kimliği toomatch hello R işlevinin herhangi bir parametre yok. Merhaba zip dosyası otomatik olarak ayıklanan toohello R çalışma dizini olmasıdır.

**Giriş kuralları:**

* Merhaba hello değerini **kimliği** hello özniteliği **giriş** öğesi geçerli bir R değişken adı olması gerekir.
* Merhaba hello değerini **kimliği** hello özniteliği **giriş** öğesi 64 karakterden uzun olmamalıdır.
* Merhaba hello değerini **adı** hello özniteliği **giriş** öğesi 64 karakterden uzun olmamalıdır.
* Merhaba Merhaba içeriğine **açıklama** öğesi 128 karakterden uzun olmamalıdır
* Merhaba hello değerini **türü** hello özniteliği **giriş** öğesi olmalıdır *Zip* veya *DataTable*.
* Merhaba hello değerini **isteğe bağlıdır** hello özniteliği **giriş** öğesi gerekli değildir (ve *false* belirtilmemişse varsayılan olarak); ancak belirtilirse, olmalıdır*true* veya *false*.

### <a name="output-elements"></a>Çıktı öğeleri
**Standart çıktı bağlantı noktaları:** çıkış bağlantı noktaları ardından sonraki modülleri tarafından kullanılan, R işlevi dönüş değerleri eşlenen toohello olduğunu. *DataTable* hello yalnızca standart çıkış bağlantı noktasına türü şu anda desteklenmiyor. (Desteği *Öğrencileriyle* ve *dönüştüren* gelecek olan.) A *DataTable* çıktı olarak tanımlanır:

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

Özel R modülleri çıktılarında için başlangıç değerini hello **kimliği** özniteliğinde hello R betiği toocorrespond ile herhangi bir şey yok ancak benzersiz olmalıdır. Tek modülü çıktı için hello dönüş değeri hello R işlevden olmalıdır bir *data.frame*. Desteklenen veri türünde birden fazla nesne toooutput sipariş, hello XML tanım dosyasında belirtilen toobe hello uygun çıkış bağlantı noktaları gerekir ve bir liste olarak döndürülen toobe hello nesnelerin gerekir. Merhaba çıkış nesnelerini toooutput bağlantı noktalarını hello nesneleri listesi döndürdü hello yerleştirilir hello sipariş yansıtma sol tooright atanır.

Toomodify hello isterseniz, örneğin, **özel Add Rows** modülü toooutput hello özgün iki veri kümesi, *dataset1* ve *dataset2*, ayrıca toohello yeni alanına katılmış veri kümesi, *dataset*, (sol tooright ile bir sırada olarak: *dataset*, *dataset1*, *dataset2*), hello tanımlayın aşağıdaki gibi çıkış bağlantı noktasına hello CustomAddRows.xml dosyasında:

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


Ve 'CustomAddRows.R' hello doğru sırayla bir listedeki hello nesnelerinin listesini döndürür:

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

**Görselleştirme çıktı:** türü bir çıkış bağlantı noktasına da belirtebilirsiniz *görselleştirme*, hello R grafik cihaz ve konsol çıkışını hello çıkış görüntüler. Bu bağlantı noktası hello R işlevi çıktı parçası olmayan ve hello diğer hello siparişle etkilemediğinden çıkış bağlantı noktası türleri. bir görselleştirme bağlantı noktası toohello özel modüller, tooadd eklemek bir **çıkış** değerini bir öğesiyle *görselleştirme* için kendi **türü** özniteliği:

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

**Çıkış kuralları:**

* Merhaba hello değerini **kimliği** hello özniteliği **çıkış** öğesi geçerli bir R değişken adı olması gerekir.
* Merhaba hello değerini **kimliği** hello özniteliği **çıkış** öğesi 32 karakterden uzun olmamalıdır.
* Merhaba hello değerini **adı** hello özniteliği **çıkış** öğesi 64 karakterden uzun olmamalıdır.
* Merhaba hello değerini **türü** hello özniteliği **çıkış** öğesi olmalıdır *görselleştirme*.

### <a name="arguments"></a>Bağımsız Değişkenler
Ek veri hello tanımlanan modülü parametreleri aracılığıyla toohello R işlevi geçirilebilir **bağımsız değişkenleri** öğesi. Merhaba modül seçildiğinde bu parametreler'hello Machine Learning UI hello en sağdaki Özellikler bölmesinde görüntülenir. Bağımsız değişkenler desteklenen hello türlerinden herhangi birinde olabilir veya gerekli olduğunda özel bir numaralandırma oluşturabilirsiniz. Benzer toohello **bağlantı noktalarını** öğeleri **bağımsız değişkenleri** öğeleri isteğe bağlı bir olabilir **açıklama** hello fare geldiğinizde görüntülenen hello metnini belirtir öğesi Hello parametre adı.
DefaultValue, minValue ve maxValue gibi bir modül için isteğe bağlı özellikler tooa öznitelikleri gibi tooany bağımsız değişkeni eklenebilir **özellikleri** öğesi. Merhaba geçerli özelliklerini **özellikleri** öğesi hello bağımsız değişkeni türüne bağlıdır ve desteklenen hello bağımsız değişken türleriyle hello sonraki bölümde açıklanmıştır. Merhaba değişkenleriyle **isteğe bağlıdır** çok ayarlanan özelliği**"true"** hello kullanıcı tooenter bir değer gerektirmez. Bir değer toohello bağımsız değişkeni sağlanmazsa, hello bağımsız değişkeni toohello giriş noktası işlevi aktarılmaz. İsteğe bağlı gerek toobe açıkça hello işlevi tarafından işlenmiş olan bağımsız değişkenler hello giriş noktası işlevi, örneğin varsayılan değeri NULL hello giriş noktası işlevi tanımında atanır. İsteğe bağlı bir bağımsız değişken yalnızca zorunlu kılacak bir değer hello kullanıcı tarafından sağlanıyorsa diğer bağımsız değişkeni kısıtlamaları, yani min veya Mak hello.
Girişleri ve çıkışları'te olduğu gibi her hello parametrelerinin kendileriyle ilişkilendirilmiş benzersiz kimliği değerlere sahip önemlidir. Bizim hızlı başlangıç örnek hello kimliği/parametre ilişkili olduğu *takas*.

### <a name="arg-element"></a>Arg öğesi
Hello kullanarak bir modülü parametresi tanımlı **Arg** hello alt öğesi **bağımsız değişkenleri** hello XML tanım dosyasını bölümü. Merhaba hello alt öğe ile **bağlantı noktalarını** bölümünde, hello parametrelerinde sıralamasını hello **bağımsız değişkenleri** bölümü hello UX karşılaştı hello düzeni tanımlar Merhaba parametreleri üstten aşağı aynı sipariş, bunlar tanımlanır içinde hello hello UI görünür hello XML dosyasında. Parametreler için makine öğrenme tarafından desteklenen hello türleri burada listelenir. 

**int** – bir tamsayı (32 bit) tür parametresi.

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* *İsteğe bağlı özellikler*: **min**, **max**, **varsayılan** ve **isteğe bağlıdır**

**çift** – çift tür parametresi.

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* *İsteğe bağlı özellikler*: **min**, **max**, **varsayılan** ve **isteğe bağlıdır**

**bool** – UX kutusunda onay tarafından temsil edilen bir Boolean parametresiyle

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* *İsteğe bağlı özellikler*: **varsayılan** -false ise ayarlanmadı

**dize**: standart bir dize

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* *İsteğe bağlı özellikler*: **varsayılan** ve **isteğe bağlıdır**

**ColumnPicker**: sütun seçimi parametresi. Bu tür hello UX Sütun Seçici işler. Merhaba **özelliği** öğesidir kullanılan burada toospecify hello kimliği içinden sütun seçildi, burada hello hedef bağlantı noktası türü olmalıdır hello noktasının *DataTable*. Merhaba sütun seçimi Hello sonucunu toohello R işlevi seçili hello sütun adlarını içeren bir dize listesi olarak geçirilir. 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* *Özellikler gerekli*: **portId** -eşleşme türü ile bir giriş öğesinin kimliği hello *DataTable*.
* *İsteğe bağlı özellikler*:
  
  * **allowedTypes** -filtreleri hello sütun türleri hangi, seçebilirsiniz gelen. Geçerli değerler şunlardır: 
    
    * sayısal
    * Boole değeri
    * Kategorik
    * Dize
    * Etiket
    * Özellik
    * Puan
    * Tümü
  * **Varsayılan** -hello Sütun Seçici için geçerli varsayılan seçimleri içerir: 
    
    * None
    * NumericFeature
    * NumericLabel
    * NumericScore
    * NumericAll
    * BooleanFeature
    * BooleanLabel
    * BooleanScore
    * BooleanAll
    * CategoricalFeature
    * CategoricalLabel
    * CategoricalScore
    * CategoricalAll
    * StringFeature
    * StringLabel
    * StringScore
    * StringAll
    * AllLabel
    * AllFeature
    * AllScore
    * Tümü

**Aşağı açılan**: bir kullanıcı tarafından belirtilen Enum (açılan) listesi. Merhaba açılır öğeleri hello içinde belirtilen **özellikleri** öğesini kullanarak bir **öğesi** öğesi. Merhaba **kimliği** her **öğesi** benzersiz olmalıdır ve geçerli bir R değişken. Merhaba hello değerini **adı** , bir **öğesi** gördüğünüz hello metin ve toohello R işlevi geçirilen hello değer görev yapar.

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* *İsteğe bağlı özellikler*:
  * **Varsayılan** - hello hello varsayılan özellik hello birinden bir ID değeriyle eşleşmelidir için bir değer **öğesi** öğeleri.

### <a name="auxiliary-files"></a>Yardımcı dosyalar
Özel Modül ZIP dosyasında yerleştirilen herhangi giderek toobe kullanılabilir yürütme sırasında bir dosyadır. Mevcut herhangi bir dizin yapıları korunur. Bu, yerel olarak ve Azure Machine Learning yürütme hello dosya kaynak belirleme çalışır, aynı satırları yerine olduğunu anlamına gelir. 

> [!NOTE]
> Tüm dosyaları ayıklanan too'src olduğunu fark ' tüm yola sahip olmanız gerekir böylece dizin ' src /' öneki.
> 
> 

Örneğin, NAs ile herhangi bir satır hello kümesinden tooremove istediğiniz ve ayrıca CustomAddRows çıktısı önce tüm yinelenen satırları kaldırır ve bir dosyada RemoveDupNARows.R yapan bir R işlevi zaten yazdıktan varsayalım:

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
Merhaba yardımcı dosyasında RemoveDupNARows.R hello CustomAddRows işlevi kaynak:

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

Ardından, 'CustomAddRows.R', 'CustomAddRows.xml' ve 'RemoveDupNARows.R' özel bir R modülü olarak içeren bir zip dosyası karşıya yükleyin.

## <a name="execution-environment"></a>Yürütme Ortamı
Merhaba yürütme ortamı hello R betiği için kullandığı aynı R sürümde hello hello **R betiği yürütün** modülü ve Kullan'ın aynı hello varsayılan paketler. Ek R paketleri tooyour özel modülü hello Özel Modül zip paketine ekleyerek de ekleyebilirsiniz. Yalnızca kendi R ortamında gibi bunları R komut dosyanıza yükleyin. 

**Merhaba yürütme ortamı sınırlamaları** içerir:

* Kalıcı olmayan dosya sistemi: hello özel modülü çalıştırdığınızda yazılmış dosyaları hello birden çok çalıştırmaları arasında sürdürülmez aynı modülü.
* Ağ erişim yok

