---
title: "aaaScale U-SQL yerel çalıştırma ve test etme, Azure Data Lake U-SQL SDK ile | Microsoft Docs"
description: "Nasıl toouse Azure Data Lake U-SQL SDK tooscale U-SQL işleri yerel çalıştırın ve komut satırı ve yerel istasyonunuzda programlama arabirimleri ile test öğrenin."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a>Ölçek U-SQL yerel çalıştırma ve test Azure Data Lake U-SQL SDK'sı

U-SQL betiği geliştirmeye genel toorun olduğundan ve yerel olarak test U-SQL betiği önce toocloud onu gönderin. Bu senaryo için Azure Data Lake U-SQL SDK adlı bir Nuget paketi Azure Data Lake sağlar, hangi, kolayca aracılığıyla U-SQL yerel çalıştırma ve test ölçeklendirilebilir. Ayrıca bu U-SQL test CI (sürekli tümleştirme) sistem tooautomate hello derleme ve test ile olası toointegrate olur.

İlgilendiğiniz ise nasıl toomanually yerel çalıştırın ve Azure Data Lake araçları için Visual Studio için kullanabileceğiniz sonra U-SQL betiği GUI araçları ile hata ayıklama. ' Dan daha fazla bilgi edinebilirsiniz [burada](data-lake-analytics-data-lake-tools-local-run.md).

## <a name="install-azure-data-lake-u-sql-sdk"></a>Yükleme Azure Data Lake U-SQL SDK'sı

Hello Azure Data Lake U-SQL SDK alabilirsiniz [burada](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) Nuget.org üzerinde. Ve kullanmadan önce aşağıdaki gibi bağımlılıklara sahip olduğunuzdan emin toomake gerekir.

### <a name="dependencies"></a>Bağımlılıklar

Merhaba Data Lake U-SQL SDK bağımlılıklar aşağıdaki hello gerektirir:

- [Microsoft .NET Framework 4.6 veya daha yeni](https://www.microsoft.com/download/details.aspx?id=17851).
- Microsoft Visual C++ 14 ve Windows SDK 10.0.10240.0 ya da daha yeni (adlandırılan CppSDK bu makalede). İki yolu tooget CppSDK vardır:

    - Yükleme [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou). Merhaba Program dosyaları klasörü--Örneğin, C:\Program Files (x86) \Windows Kits\10\ altında \Windows Kits\10 klasörü sahip olacaksınız. Ayrıca hello Windows 10 SDK sürüm \Windows Kits\10\Lib altında bulabilirsiniz. Bu klasörler görmüyorsanız, Visual Studio'yu yeniden yükleyin ve hello yükleme sırasında emin tooselect hello Windows 10 SDK olması. Bu Visual Studio ile yüklü varsa, hello U-SQL yerel derleyici onu otomatik olarak bulur.

    ![Visual Studio için Data Lake araçları yerel Windows 10 SDK çalıştırma](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - Yükleme [Visual Studio için Data Lake Araçları](http://aka.ms/adltoolsvs). Merhaba C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK Visual C++ ve Windows SDK dosyalarını paketlenmiş bulabilirsiniz. Bu durumda, hello U-SQL yerel derleyici hello bağımlılıkları otomatik olarak bulunamıyor. Bunun için toospecify hello CppSDK yol gerekir. Merhaba dosyaları tooanother konumu kopyalayabilir veya olduğu gibi kullanın.

## <a name="understand-basic-concepts"></a>Temel kavramları anlama

### <a name="data-root"></a>Veri kökü

Merhaba veri kök klasörü "yerel depolama" Merhaba yerel işlem hesabıdır. Eşdeğer toohello Azure Data Lake Store hesabını Data Lake Analytics hesabı değil. Tooa geçiş farklı bir veri kök tooa farklı depolama hesabı yalnızca değiştirme gibi klasörüdür. Farklı bir veri kök klasörlerle yaygın olarak paylaşılan veri tooaccess istiyorsanız, komut dosyalarınızı mutlak yollar kullanmanız gerekir. Veya dosya sistemi sembolik bağlantılar oluşturun (örneğin, **mklink** NTFS) hello veri kök klasör toopoint toohello altında paylaşılan veri.

Merhaba veri kök klasör için kullanılır:

- Veritabanları, tablolar, tablo değerli işlevler (Tvf) ve derlemeleri de dahil olmak üzere, yerel meta verileri depolar.
- Giriş hello ve U-SQL göreli yolda olarak tanımlanan çıkış yolları arayın. Göreli yollar kullanılarak kılar daha kolay toodeploy, U-SQL projeleri tooAzure.

### <a name="file-path-in-u-sql"></a>U-SQL dosya yolu

U-SQL betikleri göreli bir yol ve yerel bir mutlak yolu kullanabilirsiniz. Merhaba göreli yolu göreli toohello belirtilen veri kök klasör yoludur. Öneririz, kullan "/" olarak hello sunucu tarafı ile uyumlu komut dosyalarınızı yol ayırıcı toomake hello olduğunu. Göreli yollar ve eşdeğer mutlak yollarına bazı örnekleri aşağıda verilmiştir. Bu örneklerde, C:\LocalRunDataRoot hello veri kök klasörüdür.

|Göreli yolu|Mutlak yolu|
|-------------|-------------|
|/ABC/DEF/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|ABC/DEF/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/ABC/DEF/input.csv |D:\abc\def\input.csv|

### <a name="working-directory"></a>Çalışma dizini

Merhaba U-SQL komut dosyası yerel olarak çalışırken, bir çalışma dizini geçerli çalışma dizini altında derleme sırasında oluşturulur. Ayrıca toohello derleme çıkarır, hello çalışma zamanı dosyalarını yerel yürütme için gölge kopyalanan toothis çalışma dizini olacaktır. Çalışma dizini kök klasörünü hello "ScopeWorkDir" adı verilir ve hello dosyaları hello çalışma dizini altında aşağıdaki gibidir:

|Dizin/dosya|Dizin/dosya|Dizin/dosya|Tanım|Açıklama|
|--------------|--------------|--------------|----------|-----------|
|C6A101DDCB470506| | |Karma dize çalışma zamanı sürümü|Çalışma zamanı dosyalarını yerel yürütme için gerekli gölge kopyası|
| |Script_66AE4909AA0ED06C| |Ad script + betik yolu dizesi karma|Derleme çıktı ve yürütme günlüğü adım|
| | |\_komut dosyası\_.abr|Derleyici çıktısı|Cebiri dosyası|
| | |\_ScopeCodeGen\_. *|Derleyici çıktısı|Oluşturulan yönetilen kod|
| | |\_ScopeCodeGenEngine\_. *|Derleyici çıktısı|Oluşturulan yerel kod|
| | |Başvurulan derlemeler|Derleme başvurusu|Başvurulan derleme dosyaları|
| | |deployed_resources|Kaynak dağıtma|Kaynak dağıtım dosyaları|
| | |xxxxxxxx.xxx[1..n]\_\*. *|Yürütme günlüğü|Günlük yürütme adımları|


## <a name="use-hello-sdk-from-hello-command-line"></a>Merhaba SDK hello komut satırından kullanma

### <a name="command-line-interface-of-hello-helper-application"></a>Merhaba Yardımcısı uygulamasının komut satırı arabirimi

SDK directory\build\runtime altında LocalRunHelper.exe arabirimleri yaygın olarak kullanılan Merhaba, yerel çalıştırma toomost işlevleri sağlayan hello komut satırı yardımcı uygulamasıdır. Her ikisi de komut hello ve hello değişken anahtarları büyük/küçük harfe duyarlıdır unutmayın. tooinvoke onu:

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

Bağımsız değişkenler olmadan veya hello LocalRunHelper.exe çalıştırın **yardımcı** geçiş tooshow hello Yardım bilgileri:

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

Hello bilgi yardımcı olur:

-  **Komut** hello komut adını verir.  
-  **Bağımsız değişkeni gerekli** sağlanmalıdır bağımsız değişkenleri listeler.  
-  **İsteğe bağlı bağımsız değişkeni** varsayılan değerlerle isteğe bağlı bağımsız değişkenler listelenmiştir.  Boole isteğe bağlı bağımsız değişkenler parametreleri yoktur ve negatif tootheir varsayılan değer, görünümlerini anlamına gelir.

### <a name="return-value-and-logging"></a>Dönüş değeri ve günlüğe kaydetme

Merhaba yardımcı uygulama döndürür **0** başarı için ve **-1** hatası. Varsayılan olarak, tüm iletileri toohello geçerli konsol hello Yardımcısı gönderir. Ancak, hello hello komutlarının çoğunu destekler **- MessageOut path_to_log_file** hello yönlendiren isteğe bağlı bağımsız değişkeni tooa günlük dosyasına çıkarır.

### <a name="environment-variable-configuring"></a>Ortam değişkeni yapılandırma

U-SQL yerel ihtiyaçlarını bağımlılıklar için belirtilen CppSDK yolu yanı sıra yerel depolama hesabı olarak belirtilen veri kök çalıştırın. Bunlar için her iki kümesi hello bağımsız komut satırı veya ayarlanan ortam değişkeninde olabilir.

- Set hello **SCOPE_CPP_SDK** ortam değişkeni.

    Visual Studio için Data Lake araçları yükleyerek Microsoft Visual C++ ve Windows SDK hello alırsanız klasörü aşağıdaki hello sahip olduğunu doğrulayın:

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    Adlı yeni bir ortam değişkeni tanımlamak **SCOPE_CPP_SDK** toopoint toothis dizini. Veya hello klasörü toohello başka bir konuma kopyalayın ve belirtin **SCOPE_CPP_SDK** olarak.

    Toplama toosetting hello ortam değişkeninde hello belirtebilirsiniz **- CppSDK** hello komut satırı kullanırken bağımsız değişkeni. Bu bağımsız değişken varsayılan CppSDK ortam değişkeni üzerine yazar.

- Set hello **LOCALRUN_DATAROOT** ortam değişkeni.

    Adlı yeni bir ortam değişkeni tanımlamak **LOCALRUN_DATAROOT** toohello veri kök işaret.

    Toplama toosetting hello ortam değişkeninde hello belirtebilirsiniz **- DataRoot** bağımsız değişkeni ile komut satırını kullanırken hello veri kök yolu. Bu bağımsız değişken varsayılan veri kök ortam değişkeni üzerine yazar. Böylece hello varsayılan veri kök ortam değişkeni tüm işlemleri için üzerine çalıştırıyorsanız bu bağımsız değişken tooevery komut satırı tooadd gerekir.

### <a name="sdk-command-line-usage-samples"></a>SDK komut satırı kullanım örnekleri

#### <a name="compile-and-run"></a>Derleyin ve çalıştırın

Merhaba **çalıştırmak** komutu kullanıldığında toocompile hello komut dosyası ve sonra derlenmiş sonuçları yürütün. Komut satırı bağımsız değişkenlerini olanlardan birleşimidir **derleme** ve **yürütme**.

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

Hello için isteğe bağlı bağımsız değişkenler şunlardır **çalıştırmak**:


|Bağımsız değişken|Varsayılan değer|Açıklama|
|--------|-------------|-----------|
|-Arkasındaki koda|False|arka plan .cs kod Hello komut dosyası var|
|-CppSDK| |CppSDK dizini|
|-DataRoot| DataRoot ortam değişkeni|DataRoot yerel çalıştırma için varsayılan çok 'LOCALRUN_DATAROOT' ortam değişkeni|
|-MessageOut| |Konsol tooa dosyası iletilerde dökümü|
|-Paralel|1|Merhaba çalıştırmak hello planla belirtilen paralellik|
|-Başvurular| |Tarafından ayrılmış bir listesini yolları tooextra başvuru derlemeleri veya arka plan, kod veri dosyaları ';'|
|-UdoRedirect|False|Udo derleme yeniden yönlendirme yapılandırması oluşturma|
|-UseDatabase|ana|Veritabanı toouse geçici derleme kaydı arka plan kod için|
|-Verbose|False|Çalışma zamanı ayrıntılı çıkışlarından Göster|
|-WorkDir|Geçerli dizin|Derleyici kullanım ve çıktı dizini|
|-RunScopeCEP|0|ScopeCEP modu toouse|
|-ScopeCEPTempPath|Temp|Veri akışı için Geçici yol toouse|
|-OptFlags| |İyileştirici bayrakların virgülle ayrılmış listesi|


Örnek aşağıda verilmiştir:

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

Birleştirme yanı sıra **derleme** ve **yürütme**, derleyip derlenmiş hello yürütülebilir dosyalar ayrı ayrı çalıştırın.

#### <a name="compile-a-u-sql-script"></a>U-SQL komut dosyası derleme

Merhaba **derleme** kullanılan toocompile U-SQL komut dosyası tooexecutables komutudur.

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

Hello için isteğe bağlı bağımsız değişkenler şunlardır **derleme**:


|Bağımsız değişken|Açıklama|
|--------|-----------|
| -Arkasındaki koda [varsayılan değer 'False']|arka plan .cs kod Hello komut dosyası var|
| -CppSDK [varsayılan değer '']|CppSDK dizini|
| -DataRoot [varsayılan değer 'DataRoot ortam değişkeni']|DataRoot yerel çalıştırma için varsayılan çok 'LOCALRUN_DATAROOT' ortam değişkeni|
| -MessageOut [varsayılan değer '']|Konsol tooa dosyası iletilerde dökümü|
| -Başvuran [varsayılan değer '']|Tarafından ayrılmış bir listesini yolları tooextra başvuru derlemeleri veya arka plan, kod veri dosyaları ';'|
| -Basit [varsayılan değer 'False']|Basit derleme|
| -UdoRedirect [varsayılan değer 'False']|Udo derleme yeniden yönlendirme yapılandırması oluşturma|
| -UseDatabase [varsayılan değer 'master']|Veritabanı toouse geçici derleme kaydı arka plan kod için|
| -WorkDir [varsayılan değer 'Geçerli dizin']|Derleyici kullanım ve çıktı dizini|
| -RunScopeCEP [varsayılan değer '0']|ScopeCEP modu toouse|
| -ScopeCEPTempPath [varsayılan değer 'temp']|Veri akışı için Geçici yol toouse|
| -OptFlags [varsayılan değer '']|İyileştirici bayrakların virgülle ayrılmış listesi|


Bazı kullanım örnekleri aşağıda verilmiştir.

U-SQL komut dosyası derleme:

    LocalRunHelper compile -Script d:\test\test1.usql

U-SQL komut dosyasını derleyin ve hello veri kök klasörünü ayarlayın. Bu hello kümesi ortam değişkeni üzerine yazacağını unutmayın.

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

U-SQL betiği derlemek ve bir çalışma dizini, referans derlemesini ve veritabanı ayarlayın:

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>Derlenmiş sonuçları yürütme

Merhaba **yürütme** derlenmiş kullanılan tooexecute sonuçları bir komuttur.   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

Hello için isteğe bağlı bağımsız değişkenler şunlardır **yürütme**:

|Bağımsız değişken|Açıklama|
|--------|-----------|
|-DataRoot [varsayılan değer '']|Meta veri yürütme için veri kökü. Toohello varsayılan olarak **LOCALRUN_DATAROOT** ortam değişkeni.|
|-MessageOut [varsayılan değer '']|Merhaba konsol tooa dosyası iletilerde dökümü.|
|-Paralel [varsayılan değeri '1']|Gösterge toorun oluşturulan hello yerel çalıştırma hello adımlara paralellik düzeyi belirtilen.|
|-Verbose [varsayılan değer 'False']|Gösterge tooshow çalışma zamanı çıkışlarından ayrıntılı.|

Kullanım örneği aşağıdadır:

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a>Merhaba SDK ile programlama arabirimleri kullanın

Merhaba programlama arabirimleri tüm hello LocalRunHelper.exe bulunur. U-SQL komut dosyası yerel test C# test framework tooscale hello ve bunları toointegrate hello hello U-SQL SDK işlevselliğini kullanın. Bu makalede, hello standart C# birim testi projesi tooshow nasıl kullanacağım toouse bu tootest, U-SQL komut dosyası arabirimleri.

### <a name="step-1-create-c-unit-test-project-and-configuration"></a>1. adım: C# birim testi projesi ve yapılandırma oluşturma

- Dosyası aracılığıyla bir C# birim testi projesi oluşturma > Yeni > Proje > Visual C# > Test > birim testi projesi.
- Başlangıç projesi için bir başvuru olarak LocalRunHelper.exe ekleyin. Merhaba LocalRunHelper.exe \build\runtime\LocalRunHelper.exe Nuget paketi bulunur.

    ![Azure Data Lake U-SQL SDK'sı başvurusu ekleme](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- U-SQL SDK **yalnızca** destek x64 ortamı, yapma emin tooset yapı platform hedefi x64 olarak. Bu proje özelliği üzerinden ayarlayabilirsiniz > Yapı > Platform hedefi.

    ![Azure Data Lake U-SQL SDK'sını yapılandırmak x64 proje](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- Test ortamınızı emin tooset x64 olun. Visual Studio'da Test ayarlayabilirsiniz > Test Ayarları > Varsayılan İşlemci mimarisi > x64.

    ![Azure Data Lake U-SQL SDK'sını yapılandırmak x64 Test Ortamı](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- Emin toocopy genellikle ProjectFolder\bin\x64\Debug altında olan NugetPackage\build\runtime\ tooproject çalışma dizini altındaki tüm bağımlılık dosyaları olun.

### <a name="step-2-create-u-sql-script-test-case"></a>2. adım: U-SQL betiği test çalışması oluşturma

U-SQL betiği testi için hello örnek kod aşağıdadır. Test etmek için tooprepare komut dosyaları, gereken giriş dosyaları ve beklenen çıktı dosyaları.

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a>LocalRunHelper.exe programlama arabirimleri

Programlama arabirimleri çalıştırmak U-SQL yerel derleme için hello LocalRunHelper.exe sağlar, vb. hello arabirimleri aşağıda listelenmiştir.

**Oluşturucusu**

Ortak LocalRunHelper ([System.IO.TextWriter messageOutput = null])

|Parametre|Tür|Açıklama|
|---------|----|-----------|
|messageOutput|System.IO.TextWriter|Çıktı iletileri için toonull toouse konsol Ayarla|

**Özellikleri**

|Özellik|Tür|Açıklama|
|--------|----|-----------|
|AlgebraPath|Dize|Merhaba yol tooalgebra dosyası (cebiri dosya biridir hello derleme sonuçları)|
|CodeBehindReferences|Dize|Merhaba komut dosyası başvuruları arkasında ek kodu varsa, ile ayrılmış hello yollarını belirtin ';'|
|CppSdkDir|Dize|CppSDK dizini|
|CurrentDir|Dize|Geçerli dizin|
|DataRoot|Dize|Veri kök yolu|
|DebuggerMailPath|Dize|Merhaba yolu toodebugger yuvası|
|GenerateUdoRedirect|bool|Biz toogenerate derleme yüklenirken istiyorsanız yeniden yönlendirme geçersiz kılma yapılandırma|
|HasCodeBehind|bool|Merhaba betik arka plan kodu varsa|
|InputDir|Dize|Giriş verileri için dizin|
|MessagePath|Dize|İleti döküm dosyası yolu|
|OutputDir|Dize|Çıktı verileri için dizin|
|Paralellik|Int|Paralellik toorun hello cebiri|
|ParentPid|Int|PID hello üst üzerinde hangi hello tooexit, kümesi too0 veya negatif tooignore izler|
|ResultPath|Dize|Sonuç döküm dosyası yolu|
|RuntimeDir|Dize|Çalışma zamanı dizini|
|scriptPath|Dize|Burada toofind hello komut dosyası|
|Basit|bool|Derleme veya basit|
|TempDir|Dize|Geçici dizin|
|UseDataBase|Dize|Geçici derleme kaydı, varsayılan olarak ana arka plan kod için Hello veritabanı toouse belirtin|
|WorkDir|Dize|Tercih edilen çalışma dizini|


**Yöntemi**

|Yöntem|Açıklama|Döndür|Parametre|
|------|-----------|------|---------|
|Ortak bool DoCompile()|Merhaba U-SQL komut dosyası derleme|Başarı true| |
|Ortak bool DoExec()|Derlenmiş hello sonuç yürütme|Başarı true| |
|Ortak bool DoRun()|(Derleme + Execute) Hello U-SQL komut dosyasını çalıştır|Başarı true| |
|Ortak bool IsValidRuntimeDir (dize yolu)|Belirtilen yol hello geçerli çalışma zamanı yolu olup olmadığını denetleyin|TRUE olarak geçerli|çalışma zamanı dizinin Hello yolu|


## <a name="faq-about-common-issue"></a>Yaygın sorun hakkında SSS

### <a name="error-1"></a>1. hata:
E_CSC_SYSTEM_INTERNAL: İç hata oluştu! Dosya veya derleme 'ScopeEngineManaged.dll' ya da bağımlılıklarından biri yüklenemedi. Merhaba Belirtilen modül bulunamadı.

Merhaba aşağıdakileri denetleyin:

- X64 olduğundan emin olun ortamı. Merhaba yapı hedef platformu ve hello test ortamı x64 olması, çok bakın**1. adım: oluşturmak C# birim testi projesi ve yapılandırma** üstünde.
- NugetPackage\build\runtime\ tooproject çalışma dizini altındaki tüm bağımlılık dosyaları kopyalandığından emin olun.


## <a name="next-steps"></a>Sonraki adımlar

* U-SQL, toolearn bkz [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).
* toolog tanılama bilgileri bkz [Azure Data Lake Analytics için tanılama günlükleri erişme](data-lake-analytics-diagnostic-logs.md).
* toosee daha karmaşık bir sorgu görmek [Azure Data Lake Analytics'i kullanarak Web sitesi günlüklerini çözümleme](data-lake-analytics-analyze-weblogs.md).
* tooview iş ayrıntılarını görmek [kullanım iş tarayıcı ve Azure Data Lake Analytics işleri için iş görünümünde](data-lake-analytics-data-lake-tools-view-jobs.md).
* toouse hello köşe yürütme görünümü bkz [kullanım hello köşe yürütme görünümü Visual Studio için Data Lake araçları içinde](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
