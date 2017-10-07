---
title: "blob storage (Java) ile aaaOn içi uygulama | Microsoft Docs"
description: "Nasıl toocreate bir görüntü tooAzure ve görüntüler yükleyen bir konsol uygulaması hello tarayıcınızda görüntü öğrenin. Java kod örnekleri."
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a>Blob storage ile şirket içi uygulama
## <a name="overview"></a>Genel Bakış
Merhaba aşağıdaki örnek, Azure depolama ile Azure görüntüleri depolamak için nasıl kullanabileceğinizi gösterir. Bu makaledeki Hello kod bir görüntü tooAzure yükler ve ardından tarayıcınızda hello görüntü görüntüleyen bir HTML dosyası oluşturan bir konsol uygulaması içindir.

## <a name="prerequisites"></a>Ön koşullar
* Bir Java Geliştirme Seti (JDK), sürüm 1.6 veya sonraki sürümleri, yüklenir.
* Hello Azure SDK'sı yüklenir.
* Merhaba JAR hello Azure kitaplıkları için Java ve tüm geçerli bağımlılık Kavanoz yüklü olduğunu ve Java derleyicisi tarafından kullanılan hello derleme yolu bulunan. Java için Azure kitaplıkları hello yükleme hakkında daha fazla bilgi için bkz: [indirme hello Java için Azure SDK](../java-download-azure-sdk.md).
* Bir Azure depolama hesabı ayarlandığına. Merhaba hesap adı ve hesap anahtarı hello depolama hesabı için bu makaledeki hello kod tarafından kullanılır. Bkz: [nasıl tooCreate bir depolama hesabı](storage-create-storage-account.md#create-a-storage-account) bir depolama hesabı oluşturma hakkında daha fazla bilgi için ve [depolama erişim tuşlarını görüntüleme ve kopyalama](storage-create-storage-account.md#view-and-copy-storage-access-keys) hello hesap anahtarı alma hakkında bilgi.
* Adlı bir yerel görüntü dosyası oluşturdunuz hello yol c: depolanan\\myimages\\image1.jpg. Alternatif olarak, değişiklik **FileInputStream** oluşturucuda hello örnek toouse farklı görüntü yolu ve dosya adı.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a>toouse Azure blob depolama tooupload bir dosya
Adım adım bir yordam burada sunulur. Şimdi tooskip isterseniz, bu makalenin sonraki bölümlerinde hello tüm kod sunulur.

İçeri aktarmalar hello Azure çekirdek depolama sınıfları, hello Azure blob istemci sınıfları, hello Java g/ç sınıfları ve hello için ekleyerek Hello kod başlamak **URISyntaxException** sınıfı.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Adlı bir sınıf bildirme **StorageSample**ve hello açık ayraç dahil **{**.

```java
public class StorageSample {
```

Merhaba içinde **StorageSample** sınıfı, hello varsayılan uç nokta protokolü, depolama hesabınızın adını ve Azure depolama hesabınızın belirtildiği gibi depolama erişim anahtarınızı içeren bir dize değişkeni bildirin. Merhaba yer tutucu değerlerini değiştirmek **,\_hesap\_adı** ve **,\_hesap\_anahtar** hesap adı ve hesap anahtarı sırasıyla.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

İçin bildirim eklemek **ana**, içeren bir **deneyin** engelleme ve hello gerekli açık köşeli ayraçlar dahil **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

Merhaba türü (Merhaba nasıl Bu örnekte kullanıldıkları için açıklamalardır) aşağıdaki değişkenleri bildirin:

* **CloudStorageAccount**: kullanılan tooinitialize hello hesabı Azure depolama hesabı adı ve anahtar ve toocreate nesnesini blob istemci nesnesi.
* **CloudBlobClient**: tooaccess hello blob hizmeti kullanılır.
* **CloudBlobContainer**: kullanılan toocreate bir blob kapsayıcısını hello kapsayıcı ve delete hello kapsayıcısı içinde BLOB'ları listeler.
* **CloudBlockBlob**: kullanılan tooupload bir yerel görüntü dosya toothe kapsayıcısı.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Bir değer toohello Ata **hesap** değişkeni.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Bir değer toohello Ata **serviceClient** değişkeni.

```java
serviceClient = account.createCloudBlobClient();
```

Bir değer toohello Ata **kapsayıcı** değişkeni. Adlı bir başvuru tooa kapsayıcı elde edersiniz **gettingstarted**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Merhaba kapsayıcı oluşturun. Yoksa, bu yöntem hello kapsayıcı oluşturur (ve geri dönüp **true**). Merhaba kapsayıcı var olup olmadığını döndürür **false**. Alternatif çok**createIfNotExists** hello olan **oluşturma** (Merhaba kapsayıcısı zaten varsa, bir hata döndürecektir) yöntemi.

```java
container.createIfNotExists();
```

Merhaba kapsayıcısı için anonim erişimi ayarlayın.

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Azure depolama alanında hello blob temsil edecek bir başvuru toohello blok blobu alın.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Kullanım hello **dosya** Oluşturucusu tooget karşıya yükleyecek bir başvuru yerel olarak oluşturulan toohello dosyası. Merhaba kod çalıştırmadan önce bu dosyayı oluşturduktan emin olun.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Çağrı toohello aracılığıyla Hello yerel dosyayı karşıya yüklemeyi **CloudBlockBlob.upload** yöntemi. İlk parametre toohello hello **CloudBlockBlob.upload** yöntemi bir **FileInputStream** olacak o temsil hello yerel dosya karşıya tooAzure depolama nesnesi. Merhaba ikinci parametre hello hello dosyasının bayt cinsinden boyutudur.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Adlı yardımcı bir işlev çağrısı **MakeHTMLPage**, içeren toomake temel bir HTML sayfası bir  **&lt;görüntü&gt;**  Azure sunulmuştur hello kaynak kümesi toohello blob ile öğesi Depolama hesabı. Merhaba kodunu **MakeHTMLPage** bu makalenin sonraki bölümlerinde ele alınacak.

```java
MakeHTMLPage(container);
```

Bir durum iletisi ve HTML sayfası oluşturulan hello hakkında bilgi yazdırın.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

Kapat hello **deneyin** köşeli parantez ekleyerek blok: **}**

Özel durumlar aşağıdaki hello işler:

* **FileNotFoundException**: hello tarafından oluşturulan **FileInputStream** veya **FileOutputStream** oluşturucular.
* **StorageException**: hello Azure istemci depolama kitaplığı tarafından oluşturulur.
* **URISyntaxException**: hello tarafından oluşturulan **ListBlobItem.getUri** yöntemi.
* **Özel durum**: genel özel durum işleme.

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Kapat **ana** köşeli parantez ekleyerek: **}**

Adlı bir yöntem oluşturma **MakeHTMLPage** toocreate temel bir HTML sayfası. Bu yöntem türünde bir parametreye sahip **CloudBlobContainer**, karşıya yüklenen BLOB'lar hello listesi aracılığıyla kullanılan tooiterate olacaktır. Bu yöntemi özel durum türü atar **FileNotFoundException**, hangi durum hello tarafından **FileOutputStream** oluşturucusu, ve **URISyntaxException**, hangi olabilir Merhaba tarafından oluşturulan **ListBlobItem.getUri** yöntemi. Ayraç dahil **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Adlı bir yerel dosya oluşturma **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Hello ekleyerek toohello yerel dosyasını yazma  **&lt;html&gt;**,  **&lt;üstbilgi&gt;**, ve  **&lt;gövde&gt;**  öğeleri.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

Karşıya yüklenen BLOB'lar Hello listesi yineleme. Her bir blob hello HTML sayfasında oluşturma bir  **&lt;img&gt;**  olan öğeyi kendi **src** Azure depolama hesabınızdaki aldığından hello hello blob URI'si gönderilen öznitelik.
Daha eklediyseniz bu örnekte, yalnızca bir görüntü eklenen karşın, bu kod bunların tümünün yineleme.

Kolaylık olması için bu örnek karşıya yüklenen her blob bir görüntü olduğunu varsayar. BLOB'ları görüntüleri dışında ya da sayfa blobları blok blobları yerine güncelleştirdik, gerektiği gibi hello kodu ayarlayın.

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Kapat hello  **&lt;gövde&gt;**  öğesi ve hello  **&lt;html&gt;**  öğesi.

```java
stream.println("</body>");
stream.println("</html>");
```

Kapat hello yerel dosya.

```java
stream.close();
```

Kapat **MakeHTMLPage** köşeli parantez ekleyerek: **}**

Kapat **StorageSample** köşeli parantez ekleyerek: **}**

Merhaba, bu örnek için tam kod hello aşağıdadır. Toomodify hello yer tutucu değerlerini unutmayın **,\_hesap\_adı** ve **,\_hesap\_anahtar** toouse hesap adı ve hesap , sırasıyla anahtar.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

Toplama toouploading yerel görüntü dosyası tooAzure depolama hello örnek kod, tarayıcı toosee açabilirsiniz bir yerel dosya namedindex.html oluşturur, karşıya yüklenen görüntü.

Merhaba kod hesap adı ve hesap anahtarını içerdiğinden, kaynak kodunuzu güvenli olduğundan emin olun.

## <a name="toodelete-a-container"></a>toodelete bir kapsayıcı
Depolama için ücretlendirildiğinizden toodelete isteyebilirsiniz **gettingstarted** tamamladıktan sonra kapsayıcı ile bu örnek denemek. toodelete bir kapsayıcı kullanmak hello **CloudBlobContainer.delete** yöntemi.

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

toocall hello **CloudBlobContainer.delete** yöntemi, başlatma işleminin hello **CloudStorageAccount**, **ClodBlobClient**, ve  **CloudBlobContainer** nesneleri için gösterilen aynı hello olan **createIfNotExist** yöntemi. Merhaba siler adlı kapsayıcı hello tam bir örnek verilmiştir **gettingstarted**.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

Diğer blob depolama sınıflar ve yöntemler genel bakış için bkz: [nasıl toouse Java'dan Blob storage](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Sonraki adımlar
Daha karmaşık depolama görevleri hakkında daha fazla bu bağlantılar toolearn izleyin.

* [Azure depolama için Java SDK'sı](https://github.com/azure/azure-storage-java)
* [Azure Storage istemci SDK'sı başvurusu](http://dl.windowsazure.com/storage/javadoc/)
* [Azure Depolama Hizmetleri REST API'si](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure Depolama Ekibi Blog’u](http://blogs.msdn.com/b/windowsazurestorage/)

