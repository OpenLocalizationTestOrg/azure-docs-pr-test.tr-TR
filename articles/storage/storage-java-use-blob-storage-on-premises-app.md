---
title: "Şirket içi uygulama blob storage (Java) ile | Microsoft Docs"
description: "Azure'a görüntüyü yükler ve sonra görüntüyü tarayıcınızda görüntüleyen bir konsol uygulaması oluşturmayı öğrenin. Java kod örnekleri."
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
ms.openlocfilehash: a172b881fa38a69f4510df94f5797b7a56940c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="on-premises-application-with-blob-storage"></a>Blob storage ile şirket içi uygulama
## <a name="overview"></a>Genel Bakış
Aşağıdaki örnek Azure'da görüntüleri depolamak için Azure depolama nasıl kullanabileceğinizi gösterir. Bu makaledeki kod Azure'a görüntüyü yükler ve ardından tarayıcınızda görüntü görüntüleyen bir HTML dosyası oluşturan bir konsol uygulaması içindir.

## <a name="prerequisites"></a>Ön koşullar
* Bir Java Geliştirme Seti (JDK), sürüm 1.6 veya sonraki sürümleri, yüklenir.
* Azure SDK'sını yüklenir.
* Java için Azure kitaplıkları JAR ve hiçbir geçerli bağımlılık Kavanoz yüklü olduğunu ve Java derleyicisi tarafından kullanılan yapı yolu bulunan. Java için Azure kitaplıkları yükleme hakkında daha fazla bilgi için bkz: [Java için Azure SDK'sını](../java-download-azure-sdk.md).
* Bir Azure depolama hesabı ayarlandığına. Hesap adı ve hesap anahtarı depolama hesabı için bu makaledeki kod tarafından kullanılır. Bkz: [bir depolama hesabı oluşturmak nasıl](storage-create-storage-account.md#create-a-storage-account) bir depolama hesabı oluşturma hakkında daha fazla bilgi için ve [depolama erişim tuşlarını görüntüleme ve kopyalama](storage-create-storage-account.md#view-and-copy-storage-access-keys) hesap anahtarı alma hakkında bilgi.
* Adlı bir yerel görüntü dosyası oluşturdunuz yol c: depolanan\\myimages\\image1.jpg. Alternatif olarak, değişiklik **FileInputStream** farklı bir resim yolu ve dosya adını kullanmak için örnekte Oluşturucusu.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a>Bir dosyayı karşıya yüklemek için Azure blob storage kullanma
Adım adım bir yordam burada sunulur. Kodun tamamının İleri atlayabilirsiniz istiyorsanız, bu makalenin sonraki bölümlerinde sunulur.

Kod içeri aktarmalar Azure çekirdek depolama sınıfları, Azure blob istemci sınıfları, Java g/ç sınıfları için ekleyerek başlayın ve **URISyntaxException** sınıfı.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Adlı bir sınıf bildirme **StorageSample**ve açık ayraç dahil **{**.

```java
public class StorageSample {
```

İçinde **StorageSample** sınıfı, varsayılan uç nokta protokolü, depolama hesabınızın adını ve Azure depolama hesabınızın belirtildiği gibi depolama erişim anahtarınızı içeren bir dize değişkeni bildirin. Yer tutucu değerlerini değiştirmek **,\_hesap\_adı** ve **,\_hesap\_anahtar** hesap adı ve hesap anahtarı sırasıyla.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

İçin bildirim eklemek **ana**, içeren bir **deneyin** engelleme ve gerekli açık köşeli ayraçlar dahil **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

(Bunların nasıl Bu örnekte kullanıldığı için açıklamalardır) aşağıdaki türde değişkenleri bildirin:

* **CloudStorageAccount**: hesap nesnesini, Azure depolama hesabı adı ve anahtarınız ile başlatmak ve blob istemci nesnesi oluşturmak için kullanılır.
* **CloudBlobClient**: blob hizmetine erişmek için kullanılır.
* **CloudBlobContainer**: bir blob kapsayıcısını oluşturmak için kullanılan, kapsayıcıdaki blobları listelemek ve kapsayıcıyı silin.
* **CloudBlockBlob**: bir yerel görüntü dosyasını kapsayıcıya yüklemek için kullanılır.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Bir değer atadığınız **hesap** değişkeni.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Bir değer atadığınız **serviceClient** değişkeni.

```java
serviceClient = account.createCloudBlobClient();
```

Bir değer atadığınız **kapsayıcı** değişkeni. Adlı bir kapsayıcı başvurusu elde edersiniz **gettingstarted**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Kapsayıcı oluşturun. Bu yöntem yoksa kapsayıcıyı oluşturur (ve geri dönüp **true**). Kapsayıcı var olup olmadığını döndürür **false**. Alternatif **createIfNotExists** olan **oluşturma** (kapsayıcısı zaten varsa, bir hata döndürecektir) yöntemi.

```java
container.createIfNotExists();
```

Anonim erişim için kapsayıcı ayarlayın.

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Azure depolama alanında blob temsil edecek blok blob başvurusu alın.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Kullanım **dosya** karşıya yükleyecek yerel olarak oluşturulan dosyasına bir başvuru almak için Oluşturucusu. Kod çalıştırmadan önce bu dosyayı oluşturduktan emin olun.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Bir çağrı aracılığıyla yerel dosyayı karşıya yüklemeyi **CloudBlockBlob.upload** yöntemi. İlk parametre olarak **CloudBlockBlob.upload** yöntemi bir **FileInputStream** Azure depolama alanına karşıya yerel dosyayı temsil eden nesne. İkinci parametre dosyanın bayt boyutudur.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Adlı yardımcı bir işlev çağrısı **MakeHTMLPage**içeren temel bir HTML sayfası yapmak amacıyla, bir  **&lt;görüntü&gt;**  kaynağı ile öğesini ayarlamak için şu anda Azure depolama alanında blob hesabı. Kodunu **MakeHTMLPage** bu makalenin sonraki bölümlerinde ele alınacak.

```java
MakeHTMLPage(container);
```

Bir durum iletisi ve oluşturulan HTML sayfası hakkında bilgi yazdırın.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

Kapat **deneyin** köşeli parantez ekleyerek blok: **}**

Aşağıdaki özel durumları işleme:

* **FileNotFoundException**: tarafından oluşturulan **FileInputStream** veya **FileOutputStream** oluşturucular.
* **StorageException**: Azure istemci depolama kitaplığı tarafından oluşturulur.
* **URISyntaxException**: tarafından oluşturulan **ListBlobItem.getUri** yöntemi.
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

Adlı bir yöntem oluşturma **MakeHTMLPage** temel bir HTML sayfası oluşturmak için. Bu yöntem türünde bir parametreye sahip **CloudBlobContainer**, hangi karşıya yüklenen BLOB'ları listesi boyunca yinelemek için kullanılacak. Bu yöntemi özel durum türü atar **FileNotFoundException**, hangi oluşturulan tarafından **FileOutputStream** oluşturucusu, ve **URISyntaxException**, olabilen tarafından oluşturulan **ListBlobItem.getUri** yöntemi. Ayraç dahil **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Adlı bir yerel dosya oluşturma **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Ekleme yerel dosyasına yazma  **&lt;html&gt;**,  **&lt;üstbilgi&gt;**, ve  **&lt;gövde&gt;**  öğeleri.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

Karşıya yüklenen BLOB'ları listesi yineleme. HTML sayfasında bulunan her bir blob oluşturun bir  **&lt;img&gt;**  olan öğeyi kendi **src** Azure depolama hesabınızdaki aldığından BLOB URI'si gönderilen öznitelik.
Daha eklediyseniz bu örnekte, yalnızca bir görüntü eklenen karşın, bu kod bunların tümünün yineleme.

Kolaylık olması için bu örnek karşıya yüklenen her blob bir görüntü olduğunu varsayar. BLOB'ları görüntüleri dışında ya da sayfa blobları blok blobları yerine güncelleştirdik varsa, kodu gerektiği gibi ayarlayın.

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Kapat  **&lt;gövde&gt;**  öğesi ve  **&lt;html&gt;**  öğesi.

```java
stream.println("</body>");
stream.println("</html>");
```

Yerel dosyayı kapatın.

```java
stream.close();
```

Kapat **MakeHTMLPage** köşeli parantez ekleyerek: **}**

Kapat **StorageSample** köşeli parantez ekleyerek: **}**

Bu örneğin tam kodu verilmiştir. Yer tutucu değerlerini değiştirmeyi unutmayın **,\_hesap\_adı** ve **,\_hesap\_anahtar** hesap adı ve hesap anahtarını kullanmak için sırasıyla.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior to running this sample.
// Alternatively, change the value used by the FileInputStream constructor
// to use a different image path and file that you have already created.
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

            // Set anonymous access on the container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point the image is uploaded.
            // Next, create an HTML page that lists all of the uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html to see the images stored in your storage account.");

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

    // Create an HTML page that can be used to display the uploaded images.
    // This example assumes all of the blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create the opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate the uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in the HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete the <html> element and close the file.
        stream.println("</html>");
        stream.close();
    }
}
```

Azure depolama alanına yerel görüntü dosyanız karşıya ek olarak, karşıya yüklenen görüntünüzü görmek için tarayıcınızda açın bir yerel dosya namedindex.html kod örneği oluşturur.

Kod hesap adı ve hesap anahtarını içerdiğinden, kaynak kodunuzu güvenli olduğundan emin olun.

## <a name="to-delete-a-container"></a>Bir kapsayıcı silmek için
Depolama için ücretlendirildiğinizden silmek isteyebilirsiniz **gettingstarted** tamamladıktan sonra kapsayıcı ile bu örnek denemek. Bir kapsayıcı silmek için kullanın **CloudBlobContainer.delete** yöntemi.

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

Çağrılacak **CloudBlobContainer.delete** yöntemi, başlatma işlemi **CloudStorageAccount**, **ClodBlobClient**, ve **CloudBlobContainer**  nesneler olduğu için gösterilen aynı **createIfNotExist** yöntemi. Adlı kapsayıcıyı siler tam bir örnek verilmiştir **gettingstarted**.

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

Diğer blob depolama sınıflar ve yöntemler genel bakış için bkz: [Java'dan Blob storage kullanma](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Sonraki adımlar
Daha karmaşık depolama görevleri hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.

* [Azure depolama için Java SDK'sı](https://github.com/azure/azure-storage-java)
* [Azure Storage istemci SDK'sı başvurusu](http://dl.windowsazure.com/storage/javadoc/)
* [Azure Depolama Hizmetleri REST API'si](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure Depolama Ekibi Blog’u](http://blogs.msdn.com/b/windowsazurestorage/)

