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
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="baab2-104">Blob storage ile şirket içi uygulama</span><span class="sxs-lookup"><span data-stu-id="baab2-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="baab2-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="baab2-105">Overview</span></span>
<span data-ttu-id="baab2-106">Aşağıdaki örnek Azure'da görüntüleri depolamak için Azure depolama nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="baab2-106">The following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="baab2-107">Bu makaledeki kod Azure'a görüntüyü yükler ve ardından tarayıcınızda görüntü görüntüleyen bir HTML dosyası oluşturan bir konsol uygulaması içindir.</span><span class="sxs-lookup"><span data-stu-id="baab2-107">The code in this article is for a console application that uploads an image to Azure, and then creates an HTML file that displays the image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baab2-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="baab2-108">Prerequisites</span></span>
* <span data-ttu-id="baab2-109">Bir Java Geliştirme Seti (JDK), sürüm 1.6 veya sonraki sürümleri, yüklenir.</span><span class="sxs-lookup"><span data-stu-id="baab2-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="baab2-110">Azure SDK'sını yüklenir.</span><span class="sxs-lookup"><span data-stu-id="baab2-110">The Azure SDK is installed.</span></span>
* <span data-ttu-id="baab2-111">Java için Azure kitaplıkları JAR ve hiçbir geçerli bağımlılık Kavanoz yüklü olduğunu ve Java derleyicisi tarafından kullanılan yapı yolu bulunan.</span><span class="sxs-lookup"><span data-stu-id="baab2-111">The JAR for the Azure Libraries for Java, and any applicable dependency JARs, are installed and are in the build path used by your Java compiler.</span></span> <span data-ttu-id="baab2-112">Java için Azure kitaplıkları yükleme hakkında daha fazla bilgi için bkz: [Java için Azure SDK'sını](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="baab2-112">For information about installing the Azure Libraries for Java, see [Download the Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="baab2-113">Bir Azure depolama hesabı ayarlandığına.</span><span class="sxs-lookup"><span data-stu-id="baab2-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="baab2-114">Hesap adı ve hesap anahtarı depolama hesabı için bu makaledeki kod tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="baab2-114">The account name and account key for the storage account will be used by the code in this article.</span></span> <span data-ttu-id="baab2-115">Bkz: [bir depolama hesabı oluşturmak nasıl](storage-create-storage-account.md#create-a-storage-account) bir depolama hesabı oluşturma hakkında daha fazla bilgi için ve [depolama erişim tuşlarını görüntüleme ve kopyalama](storage-create-storage-account.md#view-and-copy-storage-access-keys) hesap anahtarı alma hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="baab2-115">See [How to Create a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving the account key.</span></span>
* <span data-ttu-id="baab2-116">Adlı bir yerel görüntü dosyası oluşturdunuz yol c: depolanan\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="baab2-116">You have created a local image file named stored at the path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="baab2-117">Alternatif olarak, değişiklik **FileInputStream** farklı bir resim yolu ve dosya adını kullanmak için örnekte Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="baab2-117">Alternatively, modify the **FileInputStream** constructor in the example to use a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a><span data-ttu-id="baab2-118">Bir dosyayı karşıya yüklemek için Azure blob storage kullanma</span><span class="sxs-lookup"><span data-stu-id="baab2-118">To use Azure blob storage to upload a file</span></span>
<span data-ttu-id="baab2-119">Adım adım bir yordam burada sunulur.</span><span class="sxs-lookup"><span data-stu-id="baab2-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="baab2-120">Kodun tamamının İleri atlayabilirsiniz istiyorsanız, bu makalenin sonraki bölümlerinde sunulur.</span><span class="sxs-lookup"><span data-stu-id="baab2-120">If you'd like to skip ahead, the entire code is presented later in this article.</span></span>

<span data-ttu-id="baab2-121">Kod içeri aktarmalar Azure çekirdek depolama sınıfları, Azure blob istemci sınıfları, Java g/ç sınıfları için ekleyerek başlayın ve **URISyntaxException** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="baab2-121">Begin the code by including imports for the Azure core storage classes, the Azure blob client classes, the Java IO classes, and the **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="baab2-122">Adlı bir sınıf bildirme **StorageSample**ve açık ayraç dahil **{**.</span><span class="sxs-lookup"><span data-stu-id="baab2-122">Declare a class named **StorageSample**, and include the open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="baab2-123">İçinde **StorageSample** sınıfı, varsayılan uç nokta protokolü, depolama hesabınızın adını ve Azure depolama hesabınızın belirtildiği gibi depolama erişim anahtarınızı içeren bir dize değişkeni bildirin.</span><span class="sxs-lookup"><span data-stu-id="baab2-123">Within the **StorageSample** class, declare a string variable that will contain the default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="baab2-124">Yer tutucu değerlerini değiştirmek **,\_hesap\_adı** ve **,\_hesap\_anahtar** hesap adı ve hesap anahtarı sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="baab2-124">Replace the placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="baab2-125">İçin bildirim eklemek **ana**, içeren bir **deneyin** engelleme ve gerekli açık köşeli ayraçlar dahil **{**.</span><span class="sxs-lookup"><span data-stu-id="baab2-125">Add in your declaration for **main**, include a **try** block, and include the necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="baab2-126">(Bunların nasıl Bu örnekte kullanıldığı için açıklamalardır) aşağıdaki türde değişkenleri bildirin:</span><span class="sxs-lookup"><span data-stu-id="baab2-126">Declare variables of the following type (the descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="baab2-127">**CloudStorageAccount**: hesap nesnesini, Azure depolama hesabı adı ve anahtarınız ile başlatmak ve blob istemci nesnesi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="baab2-127">**CloudStorageAccount**: Used to initialize the account object with your Azure storage account name and key, and to create the blob client object.</span></span>
* <span data-ttu-id="baab2-128">**CloudBlobClient**: blob hizmetine erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="baab2-128">**CloudBlobClient**: Used to access the blob service.</span></span>
* <span data-ttu-id="baab2-129">**CloudBlobContainer**: bir blob kapsayıcısını oluşturmak için kullanılan, kapsayıcıdaki blobları listelemek ve kapsayıcıyı silin.</span><span class="sxs-lookup"><span data-stu-id="baab2-129">**CloudBlobContainer**: Used to create a blob container, list the blobs in the container, and delete the container.</span></span>
* <span data-ttu-id="baab2-130">**CloudBlockBlob**: bir yerel görüntü dosyasını kapsayıcıya yüklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="baab2-130">**CloudBlockBlob**: Used to upload a local image file to the container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="baab2-131">Bir değer atadığınız **hesap** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="baab2-131">Assign a value to the **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="baab2-132">Bir değer atadığınız **serviceClient** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="baab2-132">Assign a value to the **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="baab2-133">Bir değer atadığınız **kapsayıcı** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="baab2-133">Assign a value to the **container** variable.</span></span> <span data-ttu-id="baab2-134">Adlı bir kapsayıcı başvurusu elde edersiniz **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="baab2-134">We'll get a reference to a container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="baab2-135">Kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="baab2-135">Create the container.</span></span> <span data-ttu-id="baab2-136">Bu yöntem yoksa kapsayıcıyı oluşturur (ve geri dönüp **true**).</span><span class="sxs-lookup"><span data-stu-id="baab2-136">This method will create the container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="baab2-137">Kapsayıcı var olup olmadığını döndürür **false**.</span><span class="sxs-lookup"><span data-stu-id="baab2-137">If the container does exist, it will return **false**.</span></span> <span data-ttu-id="baab2-138">Alternatif **createIfNotExists** olan **oluşturma** (kapsayıcısı zaten varsa, bir hata döndürecektir) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="baab2-138">An alternative to **createIfNotExists** is the **create** method (which will return an error if the container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="baab2-139">Anonim erişim için kapsayıcı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="baab2-139">Set anonymous access for the container.</span></span>

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="baab2-140">Azure depolama alanında blob temsil edecek blok blob başvurusu alın.</span><span class="sxs-lookup"><span data-stu-id="baab2-140">Get a reference to the block blob, which will represent the blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="baab2-141">Kullanım **dosya** karşıya yükleyecek yerel olarak oluşturulan dosyasına bir başvuru almak için Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="baab2-141">Use the **File** constructor to get a reference to the locally created file that you will upload.</span></span> <span data-ttu-id="baab2-142">Kod çalıştırmadan önce bu dosyayı oluşturduktan emin olun.</span><span class="sxs-lookup"><span data-stu-id="baab2-142">Ensure you have created this file before running the code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="baab2-143">Bir çağrı aracılığıyla yerel dosyayı karşıya yüklemeyi **CloudBlockBlob.upload** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="baab2-143">Upload the local file through a call to the **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="baab2-144">İlk parametre olarak **CloudBlockBlob.upload** yöntemi bir **FileInputStream** Azure depolama alanına karşıya yerel dosyayı temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="baab2-144">The first parameter to the **CloudBlockBlob.upload** method is a **FileInputStream** object that represents the local file that will be uploaded to Azure storage.</span></span> <span data-ttu-id="baab2-145">İkinci parametre dosyanın bayt boyutudur.</span><span class="sxs-lookup"><span data-stu-id="baab2-145">The second parameter is the size, in bytes, of the file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="baab2-146">Adlı yardımcı bir işlev çağrısı **MakeHTMLPage**içeren temel bir HTML sayfası yapmak amacıyla, bir  **&lt;görüntü&gt;**  kaynağı ile öğesini ayarlamak için şu anda Azure depolama alanında blob hesabı.</span><span class="sxs-lookup"><span data-stu-id="baab2-146">Call a helper function named **MakeHTMLPage**, to make a basic HTML page that contains an **&lt;image&gt;** element with the source set to the blob that is now in your Azure storage account.</span></span> <span data-ttu-id="baab2-147">Kodunu **MakeHTMLPage** bu makalenin sonraki bölümlerinde ele alınacak.</span><span class="sxs-lookup"><span data-stu-id="baab2-147">The code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="baab2-148">Bir durum iletisi ve oluşturulan HTML sayfası hakkında bilgi yazdırın.</span><span class="sxs-lookup"><span data-stu-id="baab2-148">Print out a status message and information about the created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

<span data-ttu-id="baab2-149">Kapat **deneyin** köşeli parantez ekleyerek blok: **}**</span><span class="sxs-lookup"><span data-stu-id="baab2-149">Close the **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="baab2-150">Aşağıdaki özel durumları işleme:</span><span class="sxs-lookup"><span data-stu-id="baab2-150">Handle the following exceptions:</span></span>

* <span data-ttu-id="baab2-151">**FileNotFoundException**: tarafından oluşturulan **FileInputStream** veya **FileOutputStream** oluşturucular.</span><span class="sxs-lookup"><span data-stu-id="baab2-151">**FileNotFoundException**: Can be thrown by the **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="baab2-152">**StorageException**: Azure istemci depolama kitaplığı tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="baab2-152">**StorageException**: Can be thrown by the Azure client storage library.</span></span>
* <span data-ttu-id="baab2-153">**URISyntaxException**: tarafından oluşturulan **ListBlobItem.getUri** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="baab2-153">**URISyntaxException**: Can be thrown by the **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="baab2-154">**Özel durum**: genel özel durum işleme.</span><span class="sxs-lookup"><span data-stu-id="baab2-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="baab2-155">Kapat **ana** köşeli parantez ekleyerek: **}**</span><span class="sxs-lookup"><span data-stu-id="baab2-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="baab2-156">Adlı bir yöntem oluşturma **MakeHTMLPage** temel bir HTML sayfası oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="baab2-156">Create a method named **MakeHTMLPage** to create a basic HTML page.</span></span> <span data-ttu-id="baab2-157">Bu yöntem türünde bir parametreye sahip **CloudBlobContainer**, hangi karşıya yüklenen BLOB'ları listesi boyunca yinelemek için kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="baab2-157">This method has a parameter of type **CloudBlobContainer**, which will be used to iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="baab2-158">Bu yöntemi özel durum türü atar **FileNotFoundException**, hangi oluşturulan tarafından **FileOutputStream** oluşturucusu, ve **URISyntaxException**, olabilen tarafından oluşturulan **ListBlobItem.getUri** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="baab2-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by the **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by the **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="baab2-159">Ayraç dahil **{**.</span><span class="sxs-lookup"><span data-stu-id="baab2-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="baab2-160">Adlı bir yerel dosya oluşturma **index.html**.</span><span class="sxs-lookup"><span data-stu-id="baab2-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="baab2-161">Ekleme yerel dosyasına yazma  **&lt;html&gt;**,  **&lt;üstbilgi&gt;**, ve  **&lt;gövde&gt;**  öğeleri.</span><span class="sxs-lookup"><span data-stu-id="baab2-161">Write to the local file, adding in the **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="baab2-162">Karşıya yüklenen BLOB'ları listesi yineleme.</span><span class="sxs-lookup"><span data-stu-id="baab2-162">Iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="baab2-163">HTML sayfasında bulunan her bir blob oluşturun bir  **&lt;img&gt;**  olan öğeyi kendi **src** Azure depolama hesabınızdaki aldığından BLOB URI'si gönderilen öznitelik.</span><span class="sxs-lookup"><span data-stu-id="baab2-163">For each blob, in the HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to the URI of the blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="baab2-164">Daha eklediyseniz bu örnekte, yalnızca bir görüntü eklenen karşın, bu kod bunların tümünün yineleme.</span><span class="sxs-lookup"><span data-stu-id="baab2-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="baab2-165">Kolaylık olması için bu örnek karşıya yüklenen her blob bir görüntü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="baab2-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="baab2-166">BLOB'ları görüntüleri dışında ya da sayfa blobları blok blobları yerine güncelleştirdik varsa, kodu gerektiği gibi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="baab2-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust the code as needed.</span></span>

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="baab2-167">Kapat  **&lt;gövde&gt;**  öğesi ve  **&lt;html&gt;**  öğesi.</span><span class="sxs-lookup"><span data-stu-id="baab2-167">Close the **&lt;body&gt;** element and the **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="baab2-168">Yerel dosyayı kapatın.</span><span class="sxs-lookup"><span data-stu-id="baab2-168">Close the local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="baab2-169">Kapat **MakeHTMLPage** köşeli parantez ekleyerek: **}**</span><span class="sxs-lookup"><span data-stu-id="baab2-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="baab2-170">Kapat **StorageSample** köşeli parantez ekleyerek: **}**</span><span class="sxs-lookup"><span data-stu-id="baab2-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="baab2-171">Bu örneğin tam kodu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="baab2-171">The following is the complete code for this example.</span></span> <span data-ttu-id="baab2-172">Yer tutucu değerlerini değiştirmeyi unutmayın **,\_hesap\_adı** ve **,\_hesap\_anahtar** hesap adı ve hesap anahtarını kullanmak için sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="baab2-172">Remember to modify the placeholder values **your\_account\_name** and **your\_account\_key** to use your account name and account key, respectively.</span></span>

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

<span data-ttu-id="baab2-173">Azure depolama alanına yerel görüntü dosyanız karşıya ek olarak, karşıya yüklenen görüntünüzü görmek için tarayıcınızda açın bir yerel dosya namedindex.html kod örneği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="baab2-173">In addition to uploading your local image file to Azure storage, the example code creates a local file namedindex.html, which you can open in your browser to see your uploaded image.</span></span>

<span data-ttu-id="baab2-174">Kod hesap adı ve hesap anahtarını içerdiğinden, kaynak kodunuzu güvenli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="baab2-174">Because the code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="to-delete-a-container"></a><span data-ttu-id="baab2-175">Bir kapsayıcı silmek için</span><span class="sxs-lookup"><span data-stu-id="baab2-175">To delete a container</span></span>
<span data-ttu-id="baab2-176">Depolama için ücretlendirildiğinizden silmek isteyebilirsiniz **gettingstarted** tamamladıktan sonra kapsayıcı ile bu örnek denemek.</span><span class="sxs-lookup"><span data-stu-id="baab2-176">Because you are charged for storage, you may want to delete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="baab2-177">Bir kapsayıcı silmek için kullanın **CloudBlobContainer.delete** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="baab2-177">To delete a container, use the **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="baab2-178">Çağrılacak **CloudBlobContainer.delete** yöntemi, başlatma işlemi **CloudStorageAccount**, **ClodBlobClient**, ve **CloudBlobContainer**  nesneler olduğu için gösterilen aynı **createIfNotExist** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="baab2-178">To call the **CloudBlobContainer.delete** method, the process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is the same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="baab2-179">Adlı kapsayıcıyı siler tam bir örnek verilmiştir **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="baab2-179">The following is a complete example that deletes the container named **gettingstarted**.</span></span>

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

<span data-ttu-id="baab2-180">Diğer blob depolama sınıflar ve yöntemler genel bakış için bkz: [Java'dan Blob storage kullanma](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="baab2-180">For an overview of other blob storage classes and methods, see [How to use Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="baab2-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="baab2-181">Next steps</span></span>
<span data-ttu-id="baab2-182">Daha karmaşık depolama görevleri hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="baab2-182">Follow these links to learn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="baab2-183">Azure depolama için Java SDK'sı</span><span class="sxs-lookup"><span data-stu-id="baab2-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="baab2-184">Azure Storage istemci SDK'sı başvurusu</span><span class="sxs-lookup"><span data-stu-id="baab2-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="baab2-185">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="baab2-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="baab2-186">Azure Depolama Ekibi Blog’u</span><span class="sxs-lookup"><span data-stu-id="baab2-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

