---
title: "aaaUse hello Azure Data Lake Store Java SDK'sı toodevelop uygulamaları | Microsoft Docs"
description: "Azure Data Lake Store Java SDK toocreate bir Data Lake Store hesabı kullanıp hello Data Lake Store temel işlemleri"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a>Java'yı kullanarak Azure Data Lake Store ile çalışmaya başlama
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Toouse hello Azure Data Lake Store Java SDK tooperform temel işlemleri gibi klasörleri oluşturmak nasıl öğrenin, karşıya yükleme ve indirme vb. veri dosyaları. Data Lake hakkında daha fazla bilgi için bkz. [Azure Data Lake Store](data-lake-store-overview.md).

Hello Azure Data Lake Store için Java SDK API belgeleri erişebilirsiniz [Azure Data Lake Store Java API belgeleri](https://azure.github.io/azure-data-lake-store-java/javadoc/).

## <a name="prerequisites"></a>Ön koşullar
* Java Development Kit (Java sürüm 1.7 veya üzerini kullanan JDK 7 ya da üzeri)
* Azure Data Lake Store hesabı. Merhaba yönergeleri izleyin [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).
* [Maven](https://maven.apache.org/install.html). Bu eğiticide, yapı ve proje bağımlılıkları için Maven kullanılır. Derleme Sistemi Maven veya Gradle gibi kullanmadan olası toobuild olmasına karşın, çok daha kolay toomanage bağımlılıkları olduğundan bu sistemler olun.
* (İsteğe bağlı) [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) vb. bir IDE.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Azure Active Directory'yi kullanarak nasıl kimlik doğrulaması gerçekleştiririm?
Bu öğreticide bir Azure AD uygulama istemci gizli tooretrieve bir Azure Active Directory token (hizmet kimlik doğrulaması) kullanın. Bu belirteç toocreate bir Data Lake Store istemcisi nesnesi tooperform işlemleri dosya ve dizin işlemlerini kullanırız. Nasıl kullanarak Azure Data Lake Store ile tooauthenticate hello istemci parolası ile ilgili yönergeler için aşağıdaki üst düzey adımları hello gerçekleştirin:

1. Azure AD web uygulaması oluşturma
2. Merhaba istemci kimliği, gizli ve hello Azure AD web uygulaması için belirteç uç noktası alamadı.
3. Merhaba tooaccess hello oluşturmakta olduğunuz Java uygulaması'ndan istediğiniz Data Lake Store dosya/klasör hello Azure AD web uygulamasına erişimi yapılandırın.

Yönergeler için nasıl tooperform bu adımları görmek [Active Directory Uygulama oluşturma](data-lake-store-authenticate-using-active-directory.md).

Azure Active Directory, diğer de tooretrieve bir belirteç seçenekleri sağlar. Farklı kimlik doğrulama mekanizmaları toosuit arasında bir sayı senaryonuz, örneğin, bir tarayıcı, bir masaüstü uygulaması olarak dağıtılmış bir uygulama ya da şirket içi çalıştıran bir sunucu uygulaması veya bir Azure sanal çalışan bir uygulama seçin Makine. Parolalar, sertifikalar, 2 öğeli kimlik doğrulaması vb. farklı kimlik bilgileri arasından da seçim yapabilirsiniz. Ayrıca, Azure Active Directory toosynchronize sayesinde şirket içi Active Directory kullanıcılarınıza hello bulut. Ayrıntılar için bkz. [Azure Active Directory için Kimlik Doğrulama Senaryoları](../active-directory/active-directory-authentication-scenarios.md). 

## <a name="create-a-java-application"></a>Java uygulaması oluşturma
Merhaba kod örneği [github'da](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) hello depoda dosya oluşturma, dosyaları birleştirme, dosya indirme ve hello deposundaki bazı dosyaları silin hello işleminde size yol göstermektedir. Bu bölümde hello makalenin hello ana hello kod parçalarını size yol gösterir.

1. Kullanarak bir Maven projesi oluşturun [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) gelen hello komut satırı veya bir IDE kullanma. Nasıl toocreate bir Java projesi Intellij kullanma ile ilgili yönergeler için bkz: [burada](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html). Yönergeler için Eclipse, kullanarak proje a toocreate bkz [burada](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm). 
2. Bağımlılıklar tooyour Maven aşağıdaki hello eklemek **pom.xml** dosya. Merhaba arasında metin parçacığını aşağıdaki hello eklemek  **\</VERSION >** etiketini ve hello  **\</project >** etiketi:
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    Merhaba ilk bağımlılık olan toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) hello maven depodan. İkinci bağımlılık hello (`slf4j-nop`) bu uygulama için hangi günlük framework toouse toospecify olduğu. Merhaba Data Lake Store SDK kullanan [slf4j](http://www.slf4j.org/) log4j gibi popüler günlük çerçevelerinden sayısından günlüğü, logback, vb. Java seçmenize olanak tanır günlük cephesi veya günlük yok. Bu örneğin biz günlüğü devre dışı bırakır, bu nedenle hello kullanırız **slf4j nop** bağlama. toouse, uygulamanızda diğer günlüğe kaydetme seçeneklerini görmek [burada](http://www.slf4j.org/manual.html#projectDep).

### <a name="add-hello-application-code"></a>Merhaba uygulama kodu ekleyin
Toohello kod üç ana bölümü vardır.

1. Hello Azure Active Directory belirteç edinme
2. Merhaba belirteci toocreate bir Data Lake Store istemcisi kullanın.
3. Merhaba Data Lake Store istemcisi tooperform işlemleri kullanın.

#### <a name="step-1-obtain-an-azure-active-directory-token"></a>1. Adım: Azure Active Directory belirteci edinin.
Merhaba Data Lake Store SDK hello güvenlik belirteçleri yönetmenize olanak sağlayan kullanışlı yöntemler tootalk toohello Data Lake Store hesabı gerekli sağlar. Ancak, hello SDK yalnızca bu yöntemleri kullanılmasını zorunlu kılabilir değil. Belirteç de hello kullanarak gibi almanın başka bir yöntemle kullanabilirsiniz [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), ya da kendi özel kod.

toouse hello daha önce oluşturduğunuz Merhaba Active Directory Web uygulaması için Data Lake Store SDK tooobtain belirteci hello alt sınıflarının birini kullanın `AccessTokenProvider` (Merhaba örneği kullanır `ClientCredsTokenProvider`). Merhaba belirteç sağlayıcısı önbellekleri hello kimlik bilgileri tooobtain hello belirteci kullanılan bellek ve tooexpire hakkında ise hello belirteci otomatik olarak yeniler. Kendi alt sınıflarının olası toocreate olan `AccessTokenProvider` belirteçleri müşteri kodunuz tarafından elde edilir, ancak şu an için şimdi yalnızca kullanım hello bir hello SDK sağlanan şekilde.

Değiştir **burada doldurma** hello Azure Active Directory Web uygulaması için hello gerçek değerlerle.

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a>2. Adım: Azure Data Lake Store istemci (ADLStoreClient) nesnesi oluşturma
Oluşturma bir [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) nesnesi hello son adımda oluşturulan toospecify hello Data Lake Store hesabı adı ve hello belirteç sağlayıcısı gerektirir. Bu hello Data Lake Store hesabı adı toobe bir tam etki alanı adı gerekiyor unutmayın. Örneğin, **BURAYI DOLDURUN** alanını **mydatalakestore.azuredatalakestore.net** gibi bir etki alanı adı değiştirin.

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a>3. adım: Merhaba, ADLStoreClient tooperform dosya ve dizin işlemleri kullanın
Merhaba kodunu aşağıdaki örnek kod parçacıkları bazı ortak işlemlerinin içerir. Merhaba tam bakabilirsiniz [veri Gölü deposu Java SDK API belgeleri](https://azure.github.io/azure-data-lake-store-java/javadoc/) Merhaba, **ADLStoreClient** toosee diğer işlemleri nesne.

Dosyalar, standart Java akışları kullanılarak okunur ve yazılır. Bu standart Java işlevleri (örneğin, yazdırma akışları biçimlendirilmiş çıkışı ya da herhangi bir üzerinde ek işlevsellik için hello sıkıştırma veya şifreleme akışlar için gelen toobenefit Data Lake Store akışları hello Java akışları hello üstünde hiçbirini katman anlamına gelir. Top, vs.).

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a>4. adım: Derleme ve Merhaba uygulaması çalıştırma
1. gelen toorun bir IDE içinde bulun ve basın hello **çalıştırmak** düğmesi. Maven, kullanım gelen toorun [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).
2. tooproduce hello kullanarak komut satırı derleme hello jar dahil, tüm bağımlılıklarıyla çalıştırabileceğiniz bir tek başına jar [Maven derlemesi eklenti](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html). Merhaba pom.XML hello [örnek kaynak kodu github'da](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) nasıl bir örneği olan toodo bu.

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba Java SDK'sı JavaDoc keşfedin](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [Data Lake Store'da verilerin güvenliğini sağlama](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics'i Data Lake Store ile kullanma](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight'ı Data Lake Store ile kullanma](data-lake-store-hdinsight-hadoop-use-portal.md)

