---
title: "Azure Data Lake araçları: Kullanım Azure Data Lake araçları Visual Studio kodunu | Microsoft Docs"
description: "Visual Studio Code için Azure Data Lake araçları oluşturun, test ve U-SQL betikleri çalıştırmak için nasıl kullanılacağını öğrenin. "
Keywords: "VScode, Azure Data Lake araçları, yerel çalıştırma, yerel hata ayıklama, yerel hata ayıklama, Önizleme depolama dosyası, depolama birimi yolu için karşıya yükleme"
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
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Azure Data Lake araçları Visual Studio kodunu kullanın

U-SQL komut dosyalarını çalıştırmak ve Azure Data Lake araçları Visual Studio kodunu (VS Code) oluşturmak, sınamak için nasıl kullanılacağını öğrenin. Bilgiler aşağıdaki videoda da ele alınmıştır:

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>Ön koşullar

Data Lake araçları, VS kodu tarafından desteklenen platformlarda yüklenebilir. Desteklenen platformlar, Windows, Linux ve MacOS içerir. Farklı platformlarda aşağıdaki önkoşullara sahip:

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp). Sistem ortam değişkeni yoluna java.exe yolunu ekleyin. Yapılandırma yönergeleri için bkz: [nasıl ayarlayın veya yol sistem değişkeni değiştirmeniz?]( https://www.java.com/download/help/path.xml). Yol, C:\Program Files\Java\jdk1.8.0_77\jre\bin benzer.
    - [.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).
    
- Linux (Ubuntu 14.04 LTS önerilir)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx). Kod yüklemek için aşağıdaki komutu girin:

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/). 

        - Deb paket kaynağını güncelleştirmek için aşağıdaki komutları girin:

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - Mono yüklemek için aşağıdaki komutu girin:

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Mono 4.6 desteklenmiyor. Tamamen 4.2.x yüklemeden önce sürüm 4.6 kaldırın.  

        - [Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp). Yükleme yönergeleri için bkz: [Linux 64 bit yükleme yönergeleri için Java]( https://java.com/en/download/help/linux_x64_install.xml) sayfası.
        - [.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).
- macOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/). 
    - [Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp). Yükleme yönergeleri için bkz: [Linux 64 bit yükleme yönergeleri için Java](https://java.com/en/download/help/mac_install.xml) sayfası.
    - [.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Data Lake araçları yükleme

Önkoşulları yüklendikten sonra VS Code için Data Lake araçları yükleyebilirsiniz.

**Data Lake araçları yüklemek için**

1. Visual Studio Code'da açın.
2. CTRL + P seçin ve ardından aşağıdaki komutu girin:
```
ext install usql-vscode-ext
```
Visual Studio kod uzantılarının bir listesini görebilirsiniz. Bunlardan biri olan **Azure Data Lake Araçları**.

3. Seçin **yükleme** yanına **Azure Data Lake Araçları**. Birkaç saniye sonra **yükleme** düğmesi değişiklikler **yeniden**.
4. Seçin **yeniden** uzantısını etkinleştirmek için.
5. Seçin **Tamam** onaylamak için. Azure Data Lake araçları içinde gördüğünüz **uzantıları** bölmesi.
    ![Visual Studio kod uzantılarını bölmesi için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Azure Data Lake araçları etkinleştirme
Yeni bir .usql dosyası oluşturun veya uzantıyı etkinleştirmek için mevcut bir .usql dosyasını açın. 

## <a name="connect-to-azure"></a>Azure'a Bağlanma

Derleme ve Data Lake Analytics U-SQL betikleri çalıştırmak için önce Azure hesabınızda bağlanmanız gerekir.

**Azure'a bağlanmak için**

1.  Komut paletini açmak için Ctrl + Shift + P seçin. 
2.  Girin **ADL: oturum açma**. Oturum açma bilgileri görünür **çıkış** bölmesi.

    ![Data Lake araçları Visual Studio Code komutu paletini](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Visual Studio Code cihaz oturum açma bilgileri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. Seçin CTRL + üzerinde oturum açma URL'Sİ'ı tıklatın: oturum açma Web sayfası açmak için https://aka.ms/devicelogin. Kodu girin **G567LX42V** metin kutusuna yazın ve ardından **devam**.

   ![Visual Studio Code oturum açma için Data Lake araçları kodu yapıştırın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  Web sayfasından oturum açmak için yönergeleri izleyin. Bağlandığınızda, Azure hesap adınızı sol alt köşesindeki durum çubuğunda görünür **VS Code** penceresi. 

    > [!NOTE] 
    > İki etmen etkin hesabınız varsa, PIN kullanmak yerine telefon kimlik doğrulaması kullanmanızı öneririz.

Oturumu kapatmak için aşağıdaki komutu girin **ADL: oturum kapatma**.

## <a name="list-your-data-lake-analytics-accounts"></a>Data Lake Analytics hesaplarını listeler

Bağlantıyı sınamak için Data Lake Analytics hesaplarının bir listesini alın.

**Azure aboneliğinizin Data Lake Analytics hesaplarla listelemek için**

1. Komut paletini açmak için Ctrl + Shift + P seçin.
2. Girin **ADL: liste hesapları**. Hesapları görünür **çıkış** bölmesi.

## <a name="open-the-sample-script"></a>Örnek komut dosyasını açın
Komut palet (Ctrl + Shift + P) açın ve girin **ADL: açık örnek komut dosyası**. Bu örnek başka bir örneği açılır. Ayrıca düzenleyebilir, yapılandırmak ve bu örnek komut gönderme.

## <a name="work-with-u-sql"></a>U-SQL ile çalışma

U-SQL dosya veya U-SQL ile çalışmak için bir klasör açın.

**U-SQL projeniz için bir klasör açmak için**

1. Visual Studio koddan seçin **dosya** menüsüne ve ardından **Klasör Aç**.
2. Bir klasör belirtin ve ardından **Klasör Seç**.
3. Seçin **dosya** menüsüne ve ardından **yeni**. Adsız-1 dosyası projeye eklenir.
4. Adsız-1 dosyasına aşağıdaki kodu girin:

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

    Komut dosyası/Output klasöründe bulunan bazı veriler içeren bir departments.csv dosyası oluşturur.

5. Dosyayı Farklı Kaydet **myUSQL.usql** açılan klasörde. Bir adltools_settings.json yapılandırma dosyası projeye de eklenir.
4. Açın ve aşağıdaki özelliklere sahip adltools_settings.json yapılandırın:

    - : Bir Data Lake Analytics hesabı, Azure aboneliğinizin altında.
    - Veritabanı: Hesabınız altındaki bir veritabanı. Varsayılan değer **ana**.
    - Şema: Veritabanınızı altında bir şema. Varsayılan değer **dbo**.
    - İsteğe bağlı ayarlar:
        - Öncelik: Öncelik 1 ile-1 ile 1000 en yüksek öncelikli olarak aralıktır. Varsayılan değer **1000**.
        - Paralellik: Paralellik 1 ila 150 için aralıktır. Azure Data Lake Analytics hesabınızı izin verilen maksimum paralellik varsayılan değerdir. 
        
        > [!NOTE] 
        > Ayarları geçersiz varsa, varsayılan değerler kullanılır.

    ![Visual Studio Code yapılandırma dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    İşlem Data Lake Analytics hesabı derlemek ve U-SQL işleri çalıştırmak için gereklidir. Derleme ve U-SQL işleri çalıştırma önce bilgisayar hesabını yapılandırmanız gerekir.
    
Yapılandırma kaydedildikten sonra hesap, veritabanı ve şema bilgilerini karşılık gelen .usql dosyası sol alt köşesindeki durum çubuğunda görünür. 
 
 
Yapabilecekleriniz bir klasörü açtığınızda, bir dosyanın açılması için karşılaştırıldığında:

- Arka plan kodu dosyasını kullanın. Tek dosya modunda arka plan kodu desteklenmiyor.
- Bir yapılandırma dosyası kullanın. Bir klasörü açtığınızda, çalışma klasörü komut tek yapılandırma dosya paylaşımı.


U-SQL betiği Data Lake Analytics hizmeti aracılığıyla uzaktan derler. Çıkarırsanız **derleme** komutu, U-SQL betiği, Data Lake Analytics hesabınızı gönderilir. Daha sonra Visual Studio Code derleme sonucu alır. Uzak derleme nedeniyle, Data Lake Analytics hesabınızı yapılandırma dosyasındaki bağlanma bilgilerini listesinde Visual Studio Code gerektirir.

**U-SQL betiği derlemek için**

1. Komut paletini açmak için Ctrl + Shift + P seçin. 
2. Girin **ADL: derleme betik**. Derleme sonuçları görünür **çıkış** penceresi. Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: derleme betik** bir U-SQL işi derlemek için. Derleme sonucu görünür **çıkış** bölmesi.
 

**U-SQL betiği göndermek için**

1. Komut paletini açmak için Ctrl + Shift + P seçin. 
2. Girin **ADL: işi göndermek**.  Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: işi Gönder**. 

U-SQL işi gönderdikten sonra gönderme günlükleri görünür **çıkış** VS Code penceresinde. Gönderim başarılı olursa, proje URL'si de görüntülenir. Proje URL'si gerçek zamanlı iş durumunu izlemek için bir web tarayıcısı açabilirsiniz.

İş ayrıntılarını çıktısını etkinleştirmek için ayarlanmış **jobInformationOutputPath** içinde **vs code için u sql_settings.json** dosya.
 
## <a name="use-a-code-behind-file"></a>Bir arka plan kod dosyası kullanın

Tek bir U-SQL betiği ile ilişkili bir C# dosyasına bir arka plan kodu dosyasıdır. UDO, UDA, UDT ve arka plan kod dosyasına UDF için adanmış bir komut dosyası tanımlayabilirsiniz. UDO, UDA, UDT ve UDF doğrudan komut dosyası derleme ilk kaydettirmeden kullanılabilir. Kendi eşleme U-SQL komut dosyası ile aynı klasörde arka plan kod dosyasına yerleştirin. Komut dosyası xxx.usql olarak adlandırılmışsa, arka plan kodu xxx.usql.cs adlandırılır. Arka plan kodu dosyasını el ile silin, arka plan kodu özelliği, ilişkili U-SQL betiği için devre dışı bırakılır. U-SQL betiği için müşteri kod yazma hakkında daha fazla bilgi için bkz: [yazma ve özel kodda kullanarak U-SQL: kullanıcı tanımlı işlevler]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).

Arka plan kodu desteklemek için bir çalışma klasörü açmanız gerekir. 

**Bir arka plan kod dosyası oluşturmak için**

1. Bir kaynak dosyasını açın. 
2. Komut paletini açmak için Ctrl + Shift + P seçin.
3. Girin **ADL: arka plan kod oluşturmak**. Arka plan kod dosyası, aynı klasörde oluşturulur. 

Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: kod arkasında oluşturmak**. 

Derleme ve U-SQL betiği bir arka plan kodu dosya göndermek için tek başına U-SQL betiği ile aynıdır.

Aşağıdaki iki ekran görüntüleri bir arka plan kod dosyası ve onun ilişkili U-SQL komut dosyası gösterilmektedir:
 
![Visual Studio Code arka plan kod için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Visual Studio Code arka plan kodu komut dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>Derlemeleri kullanma

Derlemeler geliştirme hakkında daha fazla bilgi için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md).

Data Lake araçları, Data Lake Analytics Kataloğu'nda özel kod derlemeleri kaydetmek için kullanabilirsiniz.

**Bir derlemeyi kaydetmek için**

Derleme aracılığıyla kaydedebilirsiniz **ADL: kaydetmek derleme** veya **ADL: kaydetmek derleme yapılandırma yoluyla** komutları.

**ADL kaydetmek için: kayıt derleme komutu**
1.  Komut paletini açmak için Ctrl + Shift + P seçin.
2.  Girin **ADL: kaydetmek derleme**. 
3.  Yerel derleme yolu belirtin. 
4.  Bir Data Lake Analytics hesabı seçin.
5.  Bir veritabanı seçin.

Sonuçları: Portal bir tarayıcıda açıldığından ve derleme kayıt işlemi görüntüler.  

Tetiklemek için kullanışlı bir başka yolu **ADL: kaydetmek derleme** komuttur dosya Gezgini'nde .dll dosyasını sağ tıklatın. 

**ADL yine de kaydetmek için: kayıt derleme yapılandırma komutu**
1.  Komut paletini açmak için Ctrl + Shift + P seçin.
2.  Girin **ADL: kaydetmek derleme yapılandırma yoluyla**. 
3.  Yerel derleme yolu belirtin. 
4.  JSON dosyası görüntülenir. Gözden geçirin ve kaynak parametreleri ve derleme bağımlılıklar gerekiyorsa düzenleyin. Yönergeler görüntülenir **çıkış** penceresi. Derleme kayıt aşamasına ilerlemek için (Ctrl + S) JSON dosyasını kaydedin.

![Visual Studio Code arka plan kod için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- Derleme bağımlılıkları: Azure Data Lake araçları autodetects DLL bağımlılıkları sahip olup olmadığını belirler. Algılandıkları sonra bağımlılıkları JSON dosyasında görüntülenir. 
>- Kaynaklar: Derleme kaydı bir parçası olarak, DLL kaynakları (örneğin, .txt, .png ve .csv) karşıya yükleyebilir. 

Tetiklemek için başka bir yolu **ADL: kaydetmek derleme yapılandırma yoluyla** komuttur dosya Gezgini'nde .dll dosyasını sağ tıklatın. 

Aşağıdaki U-SQL kodu, bütünleştirilmiş çağırmayı gösterir. Örnekte, derleme adı: *test*.

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
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a>Data Lake Analytics Kataloğu'na erişme

Azure'a bağlandıktan sonra U-SQL Kataloğu'na erişmek için aşağıdaki adımları kullanabilirsiniz.

**Azure Data Lake Analytics meta verilerine erişmek için**

1.  Ctrl + Shift + P seçin ve ardından girin **ADL: liste tabloları**.
2.  Data Lake Analytics hesaplardan birini seçin.
3.  Data Lake Analytics veritabanlarından birini seçin.
4.  Şemalar birini seçin. Tabloların listesini görebilirsiniz.

## <a name="view-data-lake-analytics-jobs"></a>Görünüm Data Lake Analytics işleri

**Data Lake Analytics işleri görüntülemek için**
1.  Komut palet (Ctrl + Shift + P) açın ve seçin **ADL: Göster iş**. 
2.  Bir Data Lake Analytics veya yerel bir hesap seçin. 
3.  İşleri listesini görünmesi hesabı için bekleyin.
4.  İş listesinden bir iş seçin, Data Lake araçları Azure Portalı'nda iş ayrıntılarını açar ve VS Code'da iş tanımı dosyası gösterir.

![Visual Studio kod IntelliSense nesne türleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Azure Data Lake Storage tümleştirme

Azure Data Lake Store ile ilgili komutları kullanabilirsiniz:
 - Azure Data Lake Storage kaynaklara göz atın. 
 - Azure Data Lake Storage dosyanın önizlemesini görüntüleyin.  
 - VS code'da Azure Data Lake Storage için doğrudan dosyası yükleyin. 

### <a name="list-the-storage-path"></a>Depolama alanı yolu listesi 
Depolama alanı yolu komut palet ya da sağ tıklatma listeleyebilirsiniz.

**Komut palet depolama yolundan listelemek için**

1.  Komut palet (Ctrl + Shift + P) açın ve girin **ADL: listesi depolama yolu**.

    ![Visual Studio Code listesi depolama birimi yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Depolama alanı yolu listeleme, tercih edilen yol seçin. Bu oluşturularak kullanan **bir yol girin** bir örnek olarak.

    ![Visual Studio Code depolama yolu listesine bir yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- VS Code her Data Lake Analytics hesabı son ziyaret edilen yolu tutar. Örneğin: / tt/sn.
    >- Kök yolu tarayıcısından: Seçili Data Lake Analytics hesabınızı veya yerel bir yol listesi kök yolu.
    >- Bir yol girin: Seçili Data Lake Analytics hesabınızı belirtilen yoldan veya yerel bir yol listesi.
    
3. Bir hesap, yerel yol veya bir Data Lake Analytics hesabı seçin.

    ![Daha fazla bilgi için Visual Studio Code Data Lake araçları seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. Seçin **daha fazla** daha fazla Data Lake Analytics hesaplarını listelemek ve Data Lake Analytics hesabı seçin.

    ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Bir Azure depolama yolunu girin. Örneğin, / çıktı.

    ![Data Lake araçları Visual Studio Code için depolama alanı yolu girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  Sonuçları: Komutu palet girişlerini temel yol bilgileri listeler.

    ![Data Lake araçları Visual Studio Code için depolama birimi yolu sonuçları listesi](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Sağ bağlam menüsü göreli yolu listelemek için daha kullanışlı bir yoludur.

**Sağ depolama yolundan listelemek için**

1.  Seçmek için yol dizesi sağ **listesi depolama yolu**.

       ![Visual Studio Code için Data Lake Araçları bağlam menüsü sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. Seçilen göreli yol komutu palette görünür.

   ![Data Lake araçları Visual Studio Code seçili göreli yolu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Bir hesap, yerel yol veya bir Data Lake Analytics hesabı seçin.

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  Sonuçları: Komutu palet geçerli yolu için dosya ve klasörleri listeler.

       ![Visual Studio Code listeden geçerli yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a>Depolama dosya önizleme
Depolama dosyası komutu palet ya da sağ tıklatma önizleyebilirsiniz.

**Depolama dosyası komutu palet aracılığıyla önizlemek için**

1.  Komut palet (Ctrl + Shift + P) açın ve girin **ADL: Önizleme depolama dosyası**.

       ![Visual Studio Code Önizleme depolama dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Bir hesap, yerel yol veya bir Data Lake Analytics hesabı seçin.

       ![Visual Studio Code için Data Lake araçları hesabı listesi](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Seçin **daha fazla** daha fazla Data Lake Analytics hesaplarını listelemek ve Data Lake Analytics hesabı seçin.

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Bir Azure depolama alanı yolu veya dosya girin. Örneğin, /output/SearchLog.txt.

       ![Data Lake araçları Visual Studio Code için depolama birimi yolu ve dosya girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  Sonuçları: Komutu palet girişlerini temel yol bilgileri listeler.

       ![Visual Studio Code için Data Lake araçları dosya sonucu Önizleme](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**Sağ depolama yolundan listelemek için**

1.  Bir dosyayı önizlemek için dosya yolu sağ tıklatın.

   ![Visual Studio Code için Data Lake Araçları bağlam menüsü sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Bir hesap, yerel yol veya bir Data Lake Analytics hesabı seçin.

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Sonuçları: VS Code dosya önizleme sonuçlarını görüntüler.

       ![Visual Studio Code için Data Lake araçları dosya sonucu Önizleme](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>Dosyayı karşıya yükleme 

Komutları girerek dosyaları karşıya yükleyebilir **ADL: dosyasını karşıya yükle** veya **ADL: yapılandırma yoluyla dosyasını karşıya yükle**.

**Karşıya yüklemek için yine de ADL dosyaları: karşıya dosya komutu**
1. Komut paletini açmak veya komut dosyası Düzenleyicisi'ni sağ tıklatın ve ardından girin için Ctrl + Shift + P seçin **dosyasını karşıya yükle**.
2.  Dosyayı karşıya yüklemek için yerel bir yol girin.

    ![Visual Studio Code için Data Lake araçları yerel yolu girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. Depolama alanı yolu listeleme yöntemlerden birini seçin. Bu oluşturularak kullanan **bir yol girin** bir örnek olarak.

    ![Visual Studio Code listesi depolama birimi yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- VS Code her Data Lake Analytics hesabı son ziyaret edilen yolu tutar. Örneğin: / tt/sn.
    >- Kök yolu tarayıcısından: Seçili Data Lake Analytics hesabınızı veya yerel bir yol listesi kök yolu.
    >- Bir yol girin: Seçili Data Lake Analytics hesabınızı belirtilen yoldan veya yerel bir yol listesi.

4. Bir hesap, yerel yol veya bir Data Lake Analytics hesabı seçin.

    ![Visual Studio Code için Data Lake araçları depolama sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Bir Azure depolama yolunu girin. Örneğin: / çıktı.

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Azure depolama yolunu bulun. Seçin **geçerli klasörü seç**.

    ![Data Lake araçları Visual Studio Code için bir klasör seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  Sonuçları: **çıkış** penceresi dosya karşıya yükleme durumunu görüntüler.

       ![Visual Studio Code için Data Lake araçları karşıya yükleme durumu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**Karşıya yüklemek için yine de ADL dosyaları: yapılandırma komutu aracılığıyla dosyasını karşıya yükle**
1.  Komut paletini açmak veya komut dosyası Düzenleyicisi'ni sağ tıklatın ve ardından girin için Ctrl + Shift + P seçin **yapılandırma yoluyla dosyasını karşıya yükle**.
2.  VS Code'da JSON dosyasını görüntüler. Dosya yolları girin ve aynı anda birden çok dosya yükleyin. Yönergeler görüntülenir **çıkış** penceresi. Dosyayı karşıya yüklemeye devam etmek için (Ctrl + S) JSON dosyasını kaydedin.

       ![Visual Studio Code dosya yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  Sonuçları: **çıkış** penceresi dosya karşıya yükleme durumunu görüntüler.

       ![Visual Studio Code için Data Lake araçları karşıya yükleme durumu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

Bir dosya depolama alanına yüklemek için başka bir dosyanın tam yolunu veya dosyanın göreli yolu komut dosyası Düzenleyicisi'nde sağ tıklatma menüsünden aracılığıyla yoludur. Yerel dosya yolu girin ve sonra hesabı seçin. **Çıkış** penceresi yükleme durumunu görüntüler. 

### <a name="open-azure-storage-explorer"></a>Açık Azure Storage Gezgini
Açabilirsiniz **Azure Storage Gezgini** komutu girerek **ADL: Web Azure Storage Gezgini açmak** veya sağ tıklama bağlam menüsünden seçerek.

**Azure Depolama Gezgini'ni açmak için**

1. Komut paletini açmak için Ctrl + Shift + P seçin.
2. Girin **açık Web Azure Storage Gezgini** veya göreli bir yol veya tam yolunu komut dosyası Düzenleyicisi'nde sağ tıklayın ve ardından **açık Web Azure Storage Gezgini**.
3. Bir Data Lake Analytics hesabı seçin.

Data Lake araçları Azure portalında Azure depolama yol açar. FIND yol ve dosya Web'den Önizleme.

### <a name="local-run-and-local-debug-for-windows-users"></a>Yerel çalıştırma ve yerel kullanıcılar için Windows hata ayıklama
U-SQL yerel çalıştırma yerel verilerinizi sınar ve kodunuzu Data Lake Analytics yayımlanmadan önce komut yerel olarak doğrular. Yerel hata ayıklama özelliği kodunuzu Data Lake Analytics gönderilmeden önce şu görevleri tamamlamanıza sağlar: 
- C# arka plan kod hata ayıklaması. 
- Kod üzerinden adım. 
- Komut dosyası yerel olarak doğrulayın.

Yerel çalıştırma ve yerel hata ayıklama hakkında yönergeler için bkz: [U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama](data-lake-tools-for-vscode-local-run-and-debug.md).

## <a name="additional-features"></a>Ek Özellikler

VS Code'da için Data Lake araçları aşağıdaki özellikleri destekler:

-   IntelliSense otomatik tamamlama: önerileri anahtar sözcükler, yöntemleri ve değişkenler gibi öğelerin etrafında açılır pencere görünür. Farklı simgeler farklı tip nesneyi temsil eder:

    - Scala veri türü
    - karmaşık veri türü
    - Yerleşik atama
    - .NET koleksiyonu ve sınıfları
    - C# ifadeleri
    - Yerleşik C# UDF'ler, Udo'lar ve UDAAGs 
    - U-SQL işlevleri
    - U-SQL Pencereleme işlevi
 
    ![Visual Studio kod IntelliSense nesne türleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   IntelliSense otomatik tamamlama Data Lake Analytics meta: Data Lake araçları, Data Lake Analytics meta veri bilgileri yerel olarak indirir. IntelliSense özelliği, veritabanı, şema, tablo, görünüm, tablo değerli işlevi, yordamlar ve C# derlemeleri, Data Lake Analytics meta veriler dahil olmak üzere nesneleri, otomatik olarak doldurur.
 
    ![Visual Studio kod IntelliSense meta verileri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   IntelliSense hata işaret: Data Lake araçları U-SQL ve C# için düzenleme hataları altını çizer. 
-   Sözdizimi vurgular: Data Lake araçları, değişkenleri, anahtar sözcükler, veri türü ve işlevleri gibi öğeleri ayırt etmek için farklı bir renk kullanır. 

    ![Visual Studio Code sözdizimi için Data Lake araçları vurgular](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Sonraki adımlar

- U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama için bkz: [U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama](data-lake-tools-for-vscode-local-run-and-debug.md).
- Başlama Data Lake Analytics hakkında bilgi için bkz: [Öğreticisi: Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).
- Visual Studio için Data Lake araçları hakkında bilgi için bkz: [öğretici: Visual Studio için Data Lake araçları kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).
- Derlemeler geliştirme hakkında daha fazla bilgi için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md).



