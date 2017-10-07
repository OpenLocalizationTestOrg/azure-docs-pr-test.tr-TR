---
title: "Azure Data Lake araçları: Kullanım Azure Data Lake araçları Visual Studio kodunu | Microsoft Docs"
description: "Nasıl toouse Azure Data Lake araçları Visual Studio Code toocreate için test ve U-SQL betikleri çalıştırmak öğrenin. "
Keywords: "VScode, Azure Data Lake araçları, yerel çalıştırma, yerel hata ayıklama, yerel hata ayıklama, Önizleme depolama dosyası toostorage yolu karşıya yükle"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Azure Data Lake araçları Visual Studio kodunu kullanın

Nasıl toouse Azure Data Lake araçları Visual Studio Code (VS Code) toocreate için test ve U-SQL betikleri çalıştırmak öğrenin. Merhaba bilgileri de video aşağıdaki hello ele alınmıştır:

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>Ön koşullar

Data Lake araçları, VS kodu tarafından desteklenen hello platformlarda yüklenebilir. Merhaba desteklenen platformlar, Windows, Linux ve MacOS içerir. Hello farklı platformlarda hello aşağıdaki önkoşullar vardır:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp). Merhaba java.exe yol toohello sistem ortam değişkeni yol ekleyin. Yapılandırma yönergeleri için bkz: [nasıl ayarlayın veya hello Path sistem değişkeni değiştirme?]( https://www.java.com/download/help/path.xml). Merhaba, benzer tooC:\Program Files\Java\jdk1.8.0_77\jre\bin yoludur.
    - [.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).
    
- Linux (Ubuntu 14.04 LTS önerilir)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx). tooinstall Merhaba kod, komutu aşağıdaki hello girin:

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/). 

        - tooupdate hello deb paket kaynağı, hello aşağıdaki komutları girin:

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - tooinstall Mono, komutu aşağıdaki hello girin:

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Mono 4.6 desteklenmiyor. Tamamen 4.2.x yüklemeden önce sürüm 4.6 kaldırın.  

        - [Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp). Yükleme yönergeleri için bkz: Merhaba [Linux 64 bit yükleme yönergeleri için Java]( https://java.com/en/download/help/linux_x64_install.xml) sayfası.
        - [.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).
- macOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/). 
    - [Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp). Yükleme yönergeleri için bkz: Merhaba [Linux 64 bit yükleme yönergeleri için Java](https://java.com/en/download/help/mac_install.xml) sayfası.
    - [.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Data Lake araçları yükleme

Merhaba önkoşulları yüklendikten sonra VS Code için Data Lake araçları yükleyebilirsiniz.

**tooinstall Data Lake araçları**

1. Visual Studio Code'da açın.
2. CTRL + P seçin ve ardından hello aşağıdaki komutu girin:
```
ext install usql-vscode-ext
```
Visual Studio kod uzantılarının bir listesini görebilirsiniz. Bunlardan biri olan **Azure Data Lake Araçları**.

3. Seçin **yükleme** sonraki çok**Azure Data Lake Araçları**. Birkaç saniye sonra hello **yükleme** düğmesini değişiklikleri çok**yeniden**.
4. Seçin **yeniden** tooactivate hello uzantısı.
5. Seçin **Tamam** tooconfirm. Azure Data Lake araçları hello görebilirsiniz **uzantıları** bölmesi.
    ![Visual Studio kod uzantılarını bölmesi için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Azure Data Lake araçları etkinleştirme
Yeni bir .usql dosyası oluşturun veya varolan .usql dosya tooactivate hello uzantı açın. 

## <a name="connect-tooazure"></a>TooAzure Bağlan

Derleme ve Data Lake Analytics U-SQL betikleri çalıştırmak için önce tooyour Azure hesabı bağlanmanız gerekir.

**tooconnect tooAzure**

1.  Ctrl + Shift + P tooopen hello komutu palet seçin. 
2.  Girin **ADL: oturum açma**. Merhaba oturum açma bilgilerini görünür hello **çıkış** bölmesi.

    ![Data Lake araçları Visual Studio Code komutu paletini](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Visual Studio Code cihaz oturum açma bilgileri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. Seçin CTRL + hello oturum açma URL'ı tıklatın: https://aka.ms/devicelogin tooopen hello oturum açma Web sayfası. Merhaba kodu girin **G567LX42V** hello metin kutusuna ve ardından **devam**.

   ![Visual Studio Code oturum açma için Data Lake araçları kodu yapıştırın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  Merhaba yönergeleri toosign hello Web sayfasından izleyin. Bağlandığınızda, Azure hesap adınızı hello durum çubuğunda hello sol alt köşesinde hello görüntülenir. **VS Code** penceresi. 

    > [!NOTE] 
    > İki etmen etkin hesabınız varsa, PIN kullanmak yerine telefon kimlik doğrulaması kullanmanızı öneririz.

Çıkış toosign hello komutu girin **ADL: oturum kapatma**.

## <a name="list-your-data-lake-analytics-accounts"></a>Data Lake Analytics hesaplarını listeler

tootest hello bağlantısı, bir Data Lake Analytics hesapları listesini alın.

**Azure aboneliğinizdeki toolist hello Data Lake Analytics hesapları**

1. Ctrl + Shift + P tooopen hello komutu palet seçin.
2. Girin **ADL: liste hesapları**. Merhaba hesapları görünmez hello **çıkış** bölmesi.

## <a name="open-hello-sample-script"></a>Açık hello örnek komut dosyası
Merhaba komutu palet (Ctrl + Shift + P) açın ve girin **ADL: açık örnek komut dosyası**. Bu örnek başka bir örneği açılır. Ayrıca düzenleyebilir, yapılandırmak ve bu örnek komut gönderme.

## <a name="work-with-u-sql"></a>U-SQL ile çalışma

U-SQL ile bir U-SQL dosya veya klasör toowork açın.

**U-SQL projeniz için bir klasör tooopen**

1. Visual Studio koddan hello seçin **dosya** menüsüne ve ardından **Klasör Aç**.
2. Bir klasör belirtin ve ardından **Klasör Seç**.
3. Select hello **dosya** menüsüne ve ardından **yeni**. Adsız-1 dosya toohello projesi eklenir.
4. Merhaba adsız 1 dosyasına koddan hello girin:

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    Merhaba betik hello/Output klasöründe bulunan bazı veriler içeren bir departments.csv dosyası oluşturur.

5. Merhaba dosyası olarak kaydetmeniz **myUSQL.usql** hello klasörünü açılır. Bir adltools_settings.json yapılandırma dosyası da toohello projesi eklenir.
4. Açın ve aşağıdaki özelliklere hello ile adltools_settings.json yapılandırın:

    - : Bir Data Lake Analytics hesabı, Azure aboneliğinizin altında.
    - Veritabanı: Hesabınız altındaki bir veritabanı. Merhaba varsayılandır **ana**.
    - Şema: Veritabanınızı altında bir şema. Merhaba varsayılandır **dbo**.
    - İsteğe bağlı ayarlar:
        - Öncelik: hello öncelik aralığı 1 ile 1 too1000 hello en yüksek öncelikli olarak arasındadır. Merhaba varsayılan değer **1000**.
        - Paralellik: 1 too150 hello paralellik aralıktır. Azure Data Lake Analytics hesabınızı izin verilen maksimum paralellik hello Hello varsayılan değerdir. 
        
        > [!NOTE] 
        > Hello ayarları geçersiz varsa, hello varsayılan değerler kullanılır.

    ![Visual Studio Code yapılandırma dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Data Lake Analytics hesabı bir işlem toocompile ve Çalıştır U-SQL işleri gerekli. Derleme ve U-SQL işleri çalıştırma önce hello bilgisayar hesabı yapılandırmanız gerekir.
    
Merhaba yapılandırma kaydedildikten sonra hello hesap, veritabanı ve şema bilgilerini hello sol alt köşesindeki hello karşılık gelen .usql dosyası hello durum çubuğunda görünür. 
 
 
Karşılaştırılan tooopening yapabileceğiniz bir klasörü açtığınızda, bir dosya:

- Arka plan kodu dosyasını kullanın. Arka plan kodu Hello tek dosya modunda desteklenmiyor.
- Bir yapılandırma dosyası kullanın. Bir klasörü açtığınızda, çalışma klasörü hello hello betiklerde tek yapılandırma dosya paylaşımı.


U-SQL betiği Hello hello Data Lake Analytics hizmeti uzaktan derler. Merhaba çıkarırsanız **derleme** komutunu hello U-SQL betiği tooyour Data Lake Analytics hesabı gönderilir. Daha sonra Visual Studio Code hello derleme sonucu alır. Toohello uzak derleme, Visual Studio Code tooconnect tooyour hello yapılandırma dosyasında Data Lake Analytics hesabı hello bilgileri listelemek gerektirir.

**toocompile U-SQL komut dosyası**

1. Ctrl + Shift + P tooopen hello komutu palet seçin. 
2. Girin **ADL: derleme betik**. Merhaba derleme sonuçları görünen hello **çıkış** penceresi. Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: derleme betik** toocompile U-SQL işi. Merhaba derleme sonucu görünür hello **çıkış** bölmesi.
 

**toosubmit U-SQL komut dosyası**

1. Ctrl + Shift + P tooopen hello komutu palet seçin. 
2. Girin **ADL: işi göndermek**.  Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: işi Gönder**. 

U-SQL işi gönderdikten sonra hello gönderimi günlükleri hello görünür **çıkış** VS Code penceresinde. Merhaba gönderme başarılı olursa, hello iş URL de görüntülenir. Bir web tarayıcısı tootrack hello gerçek zamanlı iş durumu hello iş URL açabilirsiniz.

Merhaba iş ayrıntıları, tooenable hello çıktısı ayarlamak **jobInformationOutputPath** hello içinde **vs code hello u-sql_settings.json için** dosya.
 
## <a name="use-a-code-behind-file"></a>Bir arka plan kod dosyası kullanın

Tek bir U-SQL betiği ile ilişkili bir C# dosyasına bir arka plan kodu dosyasıdır. Ayrılmış betik tooUDO, UDA, UDT ve UDF hello arka plan kod dosyasına tanımlayabilirsiniz. Merhaba UDO, UDA, UDT ve UDF doğrudan hello komut dosyasında hello derleme ilk kaydettirmeden kullanılabilir. Merhaba arka plan kod dosyasına hello aynı yerleştirileceği klasörü kendi eşleme U-SQL komut dosyası olarak. Merhaba betik xxx.usql olarak adlandırılmışsa hello arka plan kod xxx.usql.cs adlandırılır. Merhaba arka plan kodu dosyasını el ile silin, hello arka plan kodu özelliği, ilişkili U-SQL betiği için devre dışı bırakılır. U-SQL betiği için müşteri kod yazma hakkında daha fazla bilgi için bkz: [yazma ve özel kodda kullanarak U-SQL: kullanıcı tanımlı işlevler]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).

toosupport arka plan kod, bir çalışma klasörü açmanız gerekir. 

**toogenerate bir arka plan kod dosyası**

1. Bir kaynak dosyasını açın. 
2. Ctrl + Shift + P tooopen hello komutu palet seçin.
3. Girin **ADL: arka plan kod oluşturmak**. Bir arka plan kod dosyası hello aynı oluşturulur klasör. 

Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: kod arkasında oluşturmak**. 

toocompile ve U-SQL betiği bir arka plan kod dosyası ile aynı hello tek başına U-SQL ile dosyası hello olduğu gönderin.

iki ekran görüntüleri aşağıdaki hello bir arka plan kod dosyası ve onun ilişkili U-SQL komut dosyası gösterilmektedir:
 
![Visual Studio Code arka plan kod için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Visual Studio Code arka plan kodu komut dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>Derlemeleri kullanma

Derlemeler geliştirme hakkında daha fazla bilgi için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md).

Data Lake araçları tooregister özel kod derlemeleri hello Data Lake Analytics Kataloğu'nda kullanabilirsiniz.

**tooregister derleme**

Merhaba derleme hello aracılığıyla kaydedebilirsiniz **ADL: kaydetmek derleme** veya **ADL: kaydetmek derleme yapılandırma yoluyla** komutları.

**Merhaba ADL aracılığıyla tooregister: kaydetmek derleme komutu**
1.  Ctrl + Shift + P tooopen hello komutu palet seçin.
2.  Girin **ADL: kaydetmek derleme**. 
3.  Merhaba yerel derleme yolu belirtin. 
4.  Bir Data Lake Analytics hesabı seçin.
5.  Bir veritabanı seçin.

Sonuçları: hello portalı bir tarayıcıda açıldığından ve hello derleme kayıt işlemi görüntüler.  

Başka bir uygun şekilde tootrigger hello **ADL: kaydetmek derleme** tooright tıklatma hello .dll dosyasının dosya Gezgini'nde bir komuttur. 

**tooregister ancak hello ADL: kaydetmek derleme yapılandırma komutu**
1.  Ctrl + Shift + P tooopen hello komutu palet seçin.
2.  Girin **ADL: kaydetmek derleme yapılandırma yoluyla**. 
3.  Merhaba yerel derleme yolu belirtin. 
4.  Merhaba JSON dosyası görüntülenir. Gözden geçirin ve gerekirse hello derleme bağımlılıkları ve kaynak parametreleri düzenleyin. Yönergeler hello görüntülenen **çıkış** penceresi. tooproceed toohello derleme kaydı (Ctrl + S) hello JSON dosyasını kaydedin.

![Visual Studio Code arka plan kod için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- Derleme bağımlılıkları: Azure Data Lake araçları autodetects hello DLL bağımlılıkları sahip olup olmadığını belirler. algılandıkları sonra hello bağımlılıkları hello JSON dosyasında görüntülenir. 
>- Kaynaklar: Hello derleme kaydı bir parçası olarak, DLL kaynakları (örneğin, .txt, .png ve .csv) karşıya yükleyebilir. 

Başka bir şekilde tootrigger hello **ADL: kaydetmek derleme yapılandırma yoluyla** tooright tıklatma hello .dll dosyasının dosya Gezgini'nde bir komuttur. 

U-SQL kodunu aşağıdaki hello gösteren nasıl toocall derleme. Merhaba örnek hello derleme adı: *test*.

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a>Merhaba Data Lake Analytics Kataloğu'na erişme

TooAzure bağlandıktan sonra aşağıdaki adımları tooaccess hello U-SQL kataloğunu hello kullanabilirsiniz.

**tooaccess hello Azure Data Lake Analytics meta verileri**

1.  Ctrl + Shift + P seçin ve ardından girin **ADL: liste tabloları**.
2.  Merhaba Data Lake Analytics hesaplardan birini seçin.
3.  Merhaba Data Lake Analytics veritabanlarından birini seçin.
4.  Merhaba şemaları birini seçin. Tabloları hello listesini görebilirsiniz.

## <a name="view-data-lake-analytics-jobs"></a>Görünüm Data Lake Analytics işleri

**tooview Data Lake Analytics işleri**
1.  Merhaba komutu palet (Ctrl + Shift + P) açıp seçin **ADL: Göster iş**. 
2.  Bir Data Lake Analytics veya yerel bir hesap seçin. 
3.  Merhaba işleri listesini hello hesap tooappear için bekleyin.
4.  İş listesinden bir iş seçin, Data Lake araçları hello Azure portal hello iş ayrıntılarını açar ve VS Code'da hello iş tanımı dosyası gösterir.

![Visual Studio kod IntelliSense nesne türleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Azure Data Lake Storage tümleştirme

Azure Data Lake Store ile ilgili komutları kullanabilirsiniz:
 - Üzerinden Hello Azure Data Lake Storage kaynaklara göz atın. 
 - Önizleme hello Azure Data Lake Storage dosyası.  
 - Merhaba karşıya tooAzure Data Lake Storage VS Code'da dosyasını doğrudan. 

### <a name="list-hello-storage-path"></a>Liste hello depolama yolu 
Merhaba depolama yolu hello komutu palet ya da sağ tıklatma listeleyebilirsiniz.

**Merhaba komutu palet üzerinden toolist hello depolama yolu**

1.  Merhaba komutu palet (Ctrl + Shift + P) açın ve girin **ADL: listesi depolama yolu**.

    ![Visual Studio Code listesi depolama birimi yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Merhaba depolama yolu listeleme, tercih edilen yol seçin. Bu oluşturularak kullanan **bir yol girin** bir örnek olarak.

    ![Visual Studio Code tek yönlü toolist hello depolama birimi yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- VS Code her Data Lake Analytics hesabı hello son ziyaret edilen yolu tutar. Örneğin: / tt/sn.
    >- Kök yolu tarayıcısından: hello listesi kök yolu, seçilen Data Lake Analytics hesabı veya yerel bir yol.
    >- Bir yol girin: Seçili Data Lake Analytics hesabınızı belirtilen yoldan veya yerel bir yol listesi.
    
3. Bir hesap hello yerel yol veya bir Data Lake Analytics hesabı seçin.

    ![Daha fazla bilgi için Visual Studio Code Data Lake araçları seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. Seçin **daha fazla** toolist daha fazla Data Lake Analytics hesapları ve Data Lake Analytics hesabı seçin.

    ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Bir Azure depolama yolunu girin. Örneğin, / çıktı.

    ![Data Lake araçları Visual Studio Code için depolama alanı yolu girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  Sonuçları: hello komutu palet girişlerini temel alarak hello yol bilgileri listeler.

    ![Data Lake araçları Visual Studio Code için depolama birimi yolu sonuçları listesi](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Toolist hello göreli yol hello olup daha kolay bir yol bağlam menüsü sağ tıklayın.

**toolist hello depolama yolundan sağ tıklayın**

1.  Merhaba yolu dizesi tooselect sağ **listesi depolama yolu**.

       ![Visual Studio Code için Data Lake Araçları bağlam menüsü sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. Merhaba seçili göreli yolu hello komutu palette görünür.

   ![Data Lake araçları Visual Studio Code seçili göreli yolu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Bir hesap hello yerel yol veya bir Data Lake Analytics hesabı seçin.

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  Sonuçları: hello komutu palet hello klasörleri ve dosyaları hello geçerli yolu için listeler.

       ![Visual Studio Code listeden hello geçerli yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a>Önizleme hello depolama dosyası
Merhaba depolama dosyasını sağ tıklatın veya hello komutu palet aracılığıyla önizleyebilirsiniz.

**Merhaba komutu palet aracılığıyla toopreview hello depolama dosyası**

1.  Merhaba komutu palet (Ctrl + Shift + P) açın ve girin **ADL: Önizleme depolama dosyası**.

       ![Visual Studio Code Önizleme depolama dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Bir hesap hello yerel yol veya bir Data Lake Analytics hesabı seçin.

       ![Visual Studio Code için Data Lake araçları hesabı listesi](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Seçin **daha fazla** toolist daha fazla Data Lake Analytics hesapları ve Data Lake Analytics hesabı seçin.

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Bir Azure depolama alanı yolu veya dosya girin. Örneğin, /output/SearchLog.txt.

       ![Data Lake araçları Visual Studio Code için depolama birimi yolu ve dosya girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  Sonuçları: hello komutu palet girişlerini temel alarak hello yol bilgileri listeler.

       ![Visual Studio Code için Data Lake araçları dosya sonucu Önizleme](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**toolist hello depolama yolundan sağ tıklayın**

1.  bir dosya toopreview hello dosya yolu sağ tıklatın.

   ![Visual Studio Code için Data Lake Araçları bağlam menüsü sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Bir hesap hello yerel yol veya bir Data Lake Analytics hesabı seçin.

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Sonuçları: VS Code hello dosyasının hello Önizleme sonuçlarını görüntüler.

       ![Visual Studio Code için Data Lake araçları dosya sonucu Önizleme](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>Dosyayı karşıya yükleme 

Merhaba komutları girerek dosyaları karşıya yükleyebilir **ADL: dosyasını karşıya yükle** veya **ADL: yapılandırma yoluyla dosyasını karşıya yükle**.

**tooupload dosyaları yine de hello ADL: karşıya dosya komutu**
1. Ctrl + Shift + P tooopen hello komutu palet seçin veya hello komut dosyası Düzenleyicisi'ni sağ tıklatın ve ardından girin **dosyasını karşıya yükle**.
2.  tooupload hello dosya, yerel bir yol girin.

    ![Visual Studio Code için Data Lake araçları yerel yolu girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. Merhaba yolları listeleme hello depolama yolunun birini seçin. Bu oluşturularak kullanan **bir yol girin** bir örnek olarak.

    ![Visual Studio Code listesi depolama birimi yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- VS Code her Data Lake Analytics hesabı hello son ziyaret edilen yolu tutar. Örneğin: / tt/sn.
    >- Kök yolu tarayıcısından: hello listesi kök yolu, seçilen Data Lake Analytics hesabı veya yerel bir yol.
    >- Bir yol girin: Seçili Data Lake Analytics hesabınızı belirtilen yoldan veya yerel bir yol listesi.

4. Bir hesap hello yerel yol veya bir Data Lake Analytics hesabı seçin.

    ![Visual Studio Code için Data Lake araçları depolama sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Bir Azure depolama yolunu girin. Örneğin: / çıktı.

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Azure depolama yolunu bulun. Seçin **geçerli klasörü seç**.

    ![Data Lake araçları Visual Studio Code için bir klasör seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  Sonuçları: Merhaba **çıkış** penceresinde hello dosya karşıya yükleme durumunu gösterir.

       ![Visual Studio Code için Data Lake araçları karşıya yükleme durumu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**tooupload dosyaları yine de hello ADL: yapılandırma komutu aracılığıyla dosyasını karşıya yükle**
1.  Ctrl + Shift + P tooopen hello komutu palet seçin veya hello komut dosyası Düzenleyicisi'ni sağ tıklatın ve ardından girin **yapılandırma yoluyla dosyasını karşıya yükle**.
2.  VS Code'da JSON dosyasını görüntüler. Dosya yolları girin ve hello adresindeki birden çok dosya karşıya yükleme aynı anda. Yönergeler hello görüntülenen **çıkış** penceresi. tooproceed tooupload hello dosyası (Ctrl + S) hello JSON dosyasını kaydedin.

       ![Visual Studio Code dosya yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  Sonuçları: Merhaba **çıkış** penceresinde hello dosya karşıya yükleme durumunu gösterir.

       ![Visual Studio Code için Data Lake araçları karşıya yükleme durumu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

Merhaba dosya toostorage olan başka bir şekilde tooupload sağ tıklatma menüsünden hello dosyanın tam yolunu veya hello komut dosyası Düzenleyicisi'nde hello dosyanın göreli yolu. Merhaba yerel dosya yolu girin ve ardından hello hesabını seçin. Merhaba **çıkış** penceresinde hello karşıya yükleme durumunu gösterir. 

### <a name="open-azure-storage-explorer"></a>Açık Azure Storage Gezgini
Açabilirsiniz **Azure Storage Gezgini** hello komutu girerek **ADL: Web Azure Storage Gezgini açmak** veya hello sağ bağlam menüsünden seçerek.

**tooopen Azure Storage Gezgini**

1. Ctrl + Shift + P tooopen hello komutu palet seçin.
2. Girin **açık Web Azure Storage Gezgini** veya göreli bir yol veya hello komut dosyası Düzenleyicisi'nde hello tam yolu sağ tıklayın ve ardından **açık Web Azure Storage Gezgini**.
3. Bir Data Lake Analytics hesabı seçin.

Data Lake araçları hello Azure portal hello Azure depolama yol açar. Merhaba dosyasından yolu ve önizleme hello hello web bulabilirsiniz.

### <a name="local-run-and-local-debug-for-windows-users"></a>Yerel çalıştırma ve yerel kullanıcılar için Windows hata ayıklama
U-SQL yerel çalıştırma yerel verilerinizi sınar ve kodunuzu yayımlanan tooData Lake Analytics önce komut yerel olarak doğrular. kodunuzu önce aşağıdaki görevler, toocomplete hello tooData Lake Analytics gönderilen hello yerel hata ayıklama özellik sağlar: 
- C# arka plan kod hata ayıklaması. 
- Merhaba kod üzerinden adım. 
- Komut dosyası yerel olarak doğrulayın.

Yerel çalıştırma ve yerel hata ayıklama hakkında yönergeler için bkz: [U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama](data-lake-tools-for-vscode-local-run-and-debug.md).

## <a name="additional-features"></a>Ek Özellikler

VS Code'da için Data Lake araçları hello aşağıdaki özellikleri destekler:

-   IntelliSense otomatik tamamlama: önerileri anahtar sözcükler, yöntemleri ve değişkenler gibi öğelerin etrafında açılır pencere görünür. Farklı simgeler farklı hello nesne türlerini temsil eder:

    - Scala veri türü
    - karmaşık veri türü
    - Yerleşik atama
    - .NET koleksiyonu ve sınıfları
    - C# ifadeleri
    - Yerleşik C# UDF'ler, Udo'lar ve UDAAGs 
    - U-SQL işlevleri
    - U-SQL Pencereleme işlevi
 
    ![Visual Studio kod IntelliSense nesne türleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   IntelliSense otomatik tamamlama Data Lake Analytics meta: Data Lake araçları hello Data Lake Analytics meta veri bilgileri yerel olarak indirir. Merhaba IntelliSense özelliği hello veritabanı, şema, tablo, görünüm, Tablo Değerli Fonksiyon, yordamlar ve hello Data Lake Analytics meta verilerden C# derlemeleri, nesneleri otomatik olarak doldurur.
 
    ![Visual Studio kod IntelliSense meta verileri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   IntelliSense hata işaret: Data Lake araçları hataları U-SQL ve C# için düzenleme hello altını çizer. 
-   Sözdizimi vurgular: Data Lake araçları değişkenleri, anahtar sözcükler, veri türü ve işlevleri gibi farklı renkler toodifferentiate öğeleri kullanır. 

    ![Visual Studio Code sözdizimi için Data Lake araçları vurgular](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Sonraki adımlar

- U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama için bkz: [U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama](data-lake-tools-for-vscode-local-run-and-debug.md).
- Başlama Data Lake Analytics hakkında bilgi için bkz: [Öğreticisi: Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).
- Visual Studio için Data Lake araçları hakkında bilgi için bkz: [öğretici: Visual Studio için Data Lake araçları kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).
- Derlemeler geliştirme hakkında daha fazla bilgi için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md).



