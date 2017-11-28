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
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="19f06-104">Blob storage ile şirket içi uygulama</span><span class="sxs-lookup"><span data-stu-id="19f06-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="19f06-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="19f06-105">Overview</span></span>
<span data-ttu-id="19f06-106">Merhaba aşağıdaki örnek, Azure depolama ile Azure görüntüleri depolamak için nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="19f06-106">hello following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="19f06-107">Bu makaledeki Hello kod bir görüntü tooAzure yükler ve ardından tarayıcınızda hello görüntü görüntüleyen bir HTML dosyası oluşturan bir konsol uygulaması içindir.</span><span class="sxs-lookup"><span data-stu-id="19f06-107">hello code in this article is for a console application that uploads an image tooAzure, and then creates an HTML file that displays hello image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19f06-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="19f06-108">Prerequisites</span></span>
* <span data-ttu-id="19f06-109">Bir Java Geliştirme Seti (JDK), sürüm 1.6 veya sonraki sürümleri, yüklenir.</span><span class="sxs-lookup"><span data-stu-id="19f06-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="19f06-110">Hello Azure SDK'sı yüklenir.</span><span class="sxs-lookup"><span data-stu-id="19f06-110">hello Azure SDK is installed.</span></span>
* <span data-ttu-id="19f06-111">Merhaba JAR hello Azure kitaplıkları için Java ve tüm geçerli bağımlılık Kavanoz yüklü olduğunu ve Java derleyicisi tarafından kullanılan hello derleme yolu bulunan.</span><span class="sxs-lookup"><span data-stu-id="19f06-111">hello JAR for hello Azure Libraries for Java, and any applicable dependency JARs, are installed and are in hello build path used by your Java compiler.</span></span> <span data-ttu-id="19f06-112">Java için Azure kitaplıkları hello yükleme hakkında daha fazla bilgi için bkz: [indirme hello Java için Azure SDK](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="19f06-112">For information about installing hello Azure Libraries for Java, see [Download hello Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="19f06-113">Bir Azure depolama hesabı ayarlandığına.</span><span class="sxs-lookup"><span data-stu-id="19f06-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="19f06-114">Merhaba hesap adı ve hesap anahtarı hello depolama hesabı için bu makaledeki hello kod tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="19f06-114">hello account name and account key for hello storage account will be used by hello code in this article.</span></span> <span data-ttu-id="19f06-115">Bkz: [nasıl tooCreate bir depolama hesabı](storage-create-storage-account.md#create-a-storage-account) bir depolama hesabı oluşturma hakkında daha fazla bilgi için ve [depolama erişim tuşlarını görüntüleme ve kopyalama](storage-create-storage-account.md#view-and-copy-storage-access-keys) hello hesap anahtarı alma hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="19f06-115">See [How tooCreate a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving hello account key.</span></span>
* <span data-ttu-id="19f06-116">Adlı bir yerel görüntü dosyası oluşturdunuz hello yol c: depolanan\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="19f06-116">You have created a local image file named stored at hello path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="19f06-117">Alternatif olarak, değişiklik **FileInputStream** oluşturucuda hello örnek toouse farklı görüntü yolu ve dosya adı.</span><span class="sxs-lookup"><span data-stu-id="19f06-117">Alternatively, modify the **FileInputStream** constructor in hello example toouse a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a><span data-ttu-id="19f06-118">toouse Azure blob depolama tooupload bir dosya</span><span class="sxs-lookup"><span data-stu-id="19f06-118">toouse Azure blob storage tooupload a file</span></span>
<span data-ttu-id="19f06-119">Adım adım bir yordam burada sunulur.</span><span class="sxs-lookup"><span data-stu-id="19f06-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="19f06-120">Şimdi tooskip isterseniz, bu makalenin sonraki bölümlerinde hello tüm kod sunulur.</span><span class="sxs-lookup"><span data-stu-id="19f06-120">If you'd like tooskip ahead, hello entire code is presented later in this article.</span></span>

<span data-ttu-id="19f06-121">İçeri aktarmalar hello Azure çekirdek depolama sınıfları, hello Azure blob istemci sınıfları, hello Java g/ç sınıfları ve hello için ekleyerek Hello kod başlamak **URISyntaxException** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="19f06-121">Begin hello code by including imports for hello Azure core storage classes, hello Azure blob client classes, hello Java IO classes, and hello **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="19f06-122">Adlı bir sınıf bildirme **StorageSample**ve hello açık ayraç dahil **{**.</span><span class="sxs-lookup"><span data-stu-id="19f06-122">Declare a class named **StorageSample**, and include hello open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="19f06-123">Merhaba içinde **StorageSample** sınıfı, hello varsayılan uç nokta protokolü, depolama hesabınızın adını ve Azure depolama hesabınızın belirtildiği gibi depolama erişim anahtarınızı içeren bir dize değişkeni bildirin.</span><span class="sxs-lookup"><span data-stu-id="19f06-123">Within hello **StorageSample** class, declare a string variable that will contain hello default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="19f06-124">Merhaba yer tutucu değerlerini değiştirmek **,\_hesap\_adı** ve **,\_hesap\_anahtar** hesap adı ve hesap anahtarı sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="19f06-124">Replace hello placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="19f06-125">İçin bildirim eklemek **ana**, içeren bir **deneyin** engelleme ve hello gerekli açık köşeli ayraçlar dahil **{**.</span><span class="sxs-lookup"><span data-stu-id="19f06-125">Add in your declaration for **main**, include a **try** block, and include hello necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="19f06-126">Merhaba türü (Merhaba nasıl Bu örnekte kullanıldıkları için açıklamalardır) aşağıdaki değişkenleri bildirin:</span><span class="sxs-lookup"><span data-stu-id="19f06-126">Declare variables of hello following type (hello descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="19f06-127">**CloudStorageAccount**: kullanılan tooinitialize hello hesabı Azure depolama hesabı adı ve anahtar ve toocreate nesnesini blob istemci nesnesi.</span><span class="sxs-lookup"><span data-stu-id="19f06-127">**CloudStorageAccount**: Used tooinitialize hello account object with your Azure storage account name and key, and toocreate the blob client object.</span></span>
* <span data-ttu-id="19f06-128">**CloudBlobClient**: tooaccess hello blob hizmeti kullanılır.</span><span class="sxs-lookup"><span data-stu-id="19f06-128">**CloudBlobClient**: Used tooaccess hello blob service.</span></span>
* <span data-ttu-id="19f06-129">**CloudBlobContainer**: kullanılan toocreate bir blob kapsayıcısını hello kapsayıcı ve delete hello kapsayıcısı içinde BLOB'ları listeler.</span><span class="sxs-lookup"><span data-stu-id="19f06-129">**CloudBlobContainer**: Used toocreate a blob container, list the blobs in hello container, and delete hello container.</span></span>
* <span data-ttu-id="19f06-130">**CloudBlockBlob**: kullanılan tooupload bir yerel görüntü dosya toothe kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="19f06-130">**CloudBlockBlob**: Used tooupload a local image file toothe container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="19f06-131">Bir değer toohello Ata **hesap** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="19f06-131">Assign a value toohello **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="19f06-132">Bir değer toohello Ata **serviceClient** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="19f06-132">Assign a value toohello **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="19f06-133">Bir değer toohello Ata **kapsayıcı** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="19f06-133">Assign a value toohello **container** variable.</span></span> <span data-ttu-id="19f06-134">Adlı bir başvuru tooa kapsayıcı elde edersiniz **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="19f06-134">We'll get a reference tooa container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="19f06-135">Merhaba kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="19f06-135">Create hello container.</span></span> <span data-ttu-id="19f06-136">Yoksa, bu yöntem hello kapsayıcı oluşturur (ve geri dönüp **true**).</span><span class="sxs-lookup"><span data-stu-id="19f06-136">This method will create hello container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="19f06-137">Merhaba kapsayıcı var olup olmadığını döndürür **false**.</span><span class="sxs-lookup"><span data-stu-id="19f06-137">If hello container does exist, it will return **false**.</span></span> <span data-ttu-id="19f06-138">Alternatif çok**createIfNotExists** hello olan **oluşturma** (Merhaba kapsayıcısı zaten varsa, bir hata döndürecektir) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="19f06-138">An alternative too**createIfNotExists** is hello **create** method (which will return an error if hello container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="19f06-139">Merhaba kapsayıcısı için anonim erişimi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="19f06-139">Set anonymous access for hello container.</span></span>

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="19f06-140">Azure depolama alanında hello blob temsil edecek bir başvuru toohello blok blobu alın.</span><span class="sxs-lookup"><span data-stu-id="19f06-140">Get a reference toohello block blob, which will represent hello blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="19f06-141">Kullanım hello **dosya** Oluşturucusu tooget karşıya yükleyecek bir başvuru yerel olarak oluşturulan toohello dosyası.</span><span class="sxs-lookup"><span data-stu-id="19f06-141">Use hello **File** constructor tooget a reference toohello locally created file that you will upload.</span></span> <span data-ttu-id="19f06-142">Merhaba kod çalıştırmadan önce bu dosyayı oluşturduktan emin olun.</span><span class="sxs-lookup"><span data-stu-id="19f06-142">Ensure you have created this file before running hello code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="19f06-143">Çağrı toohello aracılığıyla Hello yerel dosyayı karşıya yüklemeyi **CloudBlockBlob.upload** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="19f06-143">Upload hello local file through a call toohello **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="19f06-144">İlk parametre toohello hello **CloudBlockBlob.upload** yöntemi bir **FileInputStream** olacak o temsil hello yerel dosya karşıya tooAzure depolama nesnesi.</span><span class="sxs-lookup"><span data-stu-id="19f06-144">hello first parameter toohello **CloudBlockBlob.upload** method is a **FileInputStream** object that represents hello local file that will be uploaded tooAzure storage.</span></span> <span data-ttu-id="19f06-145">Merhaba ikinci parametre hello hello dosyasının bayt cinsinden boyutudur.</span><span class="sxs-lookup"><span data-stu-id="19f06-145">hello second parameter is hello size, in bytes, of hello file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="19f06-146">Adlı yardımcı bir işlev çağrısı **MakeHTMLPage**, içeren toomake temel bir HTML sayfası bir  **&lt;görüntü&gt;**  Azure sunulmuştur hello kaynak kümesi toohello blob ile öğesi Depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="19f06-146">Call a helper function named **MakeHTMLPage**, toomake a basic HTML page that contains an **&lt;image&gt;** element with hello source set toohello blob that is now in your Azure storage account.</span></span> <span data-ttu-id="19f06-147">Merhaba kodunu **MakeHTMLPage** bu makalenin sonraki bölümlerinde ele alınacak.</span><span class="sxs-lookup"><span data-stu-id="19f06-147">hello code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="19f06-148">Bir durum iletisi ve HTML sayfası oluşturulan hello hakkında bilgi yazdırın.</span><span class="sxs-lookup"><span data-stu-id="19f06-148">Print out a status message and information about hello created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

<span data-ttu-id="19f06-149">Kapat hello **deneyin** köşeli parantez ekleyerek blok: **}**</span><span class="sxs-lookup"><span data-stu-id="19f06-149">Close hello **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="19f06-150">Özel durumlar aşağıdaki hello işler:</span><span class="sxs-lookup"><span data-stu-id="19f06-150">Handle hello following exceptions:</span></span>

* <span data-ttu-id="19f06-151">**FileNotFoundException**: hello tarafından oluşturulan **FileInputStream** veya **FileOutputStream** oluşturucular.</span><span class="sxs-lookup"><span data-stu-id="19f06-151">**FileNotFoundException**: Can be thrown by hello **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="19f06-152">**StorageException**: hello Azure istemci depolama kitaplığı tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="19f06-152">**StorageException**: Can be thrown by hello Azure client storage library.</span></span>
* <span data-ttu-id="19f06-153">**URISyntaxException**: hello tarafından oluşturulan **ListBlobItem.getUri** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="19f06-153">**URISyntaxException**: Can be thrown by hello **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="19f06-154">**Özel durum**: genel özel durum işleme.</span><span class="sxs-lookup"><span data-stu-id="19f06-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="19f06-155">Kapat **ana** köşeli parantez ekleyerek: **}**</span><span class="sxs-lookup"><span data-stu-id="19f06-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="19f06-156">Adlı bir yöntem oluşturma **MakeHTMLPage** toocreate temel bir HTML sayfası.</span><span class="sxs-lookup"><span data-stu-id="19f06-156">Create a method named **MakeHTMLPage** toocreate a basic HTML page.</span></span> <span data-ttu-id="19f06-157">Bu yöntem türünde bir parametreye sahip **CloudBlobContainer**, karşıya yüklenen BLOB'lar hello listesi aracılığıyla kullanılan tooiterate olacaktır.</span><span class="sxs-lookup"><span data-stu-id="19f06-157">This method has a parameter of type **CloudBlobContainer**, which will be used tooiterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="19f06-158">Bu yöntemi özel durum türü atar **FileNotFoundException**, hangi durum hello tarafından **FileOutputStream** oluşturucusu, ve **URISyntaxException**, hangi olabilir Merhaba tarafından oluşturulan **ListBlobItem.getUri** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="19f06-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by hello **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by hello **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="19f06-159">Ayraç dahil **{**.</span><span class="sxs-lookup"><span data-stu-id="19f06-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="19f06-160">Adlı bir yerel dosya oluşturma **index.html**.</span><span class="sxs-lookup"><span data-stu-id="19f06-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="19f06-161">Hello ekleyerek toohello yerel dosyasını yazma  **&lt;html&gt;**,  **&lt;üstbilgi&gt;**, ve  **&lt;gövde&gt;**  öğeleri.</span><span class="sxs-lookup"><span data-stu-id="19f06-161">Write toohello local file, adding in hello **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="19f06-162">Karşıya yüklenen BLOB'lar Hello listesi yineleme.</span><span class="sxs-lookup"><span data-stu-id="19f06-162">Iterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="19f06-163">Her bir blob hello HTML sayfasında oluşturma bir  **&lt;img&gt;**  olan öğeyi kendi **src** Azure depolama hesabınızdaki aldığından hello hello blob URI'si gönderilen öznitelik.</span><span class="sxs-lookup"><span data-stu-id="19f06-163">For each blob, in hello HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to hello URI of hello blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="19f06-164">Daha eklediyseniz bu örnekte, yalnızca bir görüntü eklenen karşın, bu kod bunların tümünün yineleme.</span><span class="sxs-lookup"><span data-stu-id="19f06-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="19f06-165">Kolaylık olması için bu örnek karşıya yüklenen her blob bir görüntü olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="19f06-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="19f06-166">BLOB'ları görüntüleri dışında ya da sayfa blobları blok blobları yerine güncelleştirdik, gerektiği gibi hello kodu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="19f06-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust hello code as needed.</span></span>

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="19f06-167">Kapat hello  **&lt;gövde&gt;**  öğesi ve hello  **&lt;html&gt;**  öğesi.</span><span class="sxs-lookup"><span data-stu-id="19f06-167">Close hello **&lt;body&gt;** element and hello **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="19f06-168">Kapat hello yerel dosya.</span><span class="sxs-lookup"><span data-stu-id="19f06-168">Close hello local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="19f06-169">Kapat **MakeHTMLPage** köşeli parantez ekleyerek: **}**</span><span class="sxs-lookup"><span data-stu-id="19f06-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="19f06-170">Kapat **StorageSample** köşeli parantez ekleyerek: **}**</span><span class="sxs-lookup"><span data-stu-id="19f06-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="19f06-171">Merhaba, bu örnek için tam kod hello aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="19f06-171">hello following is hello complete code for this example.</span></span> <span data-ttu-id="19f06-172">Toomodify hello yer tutucu değerlerini unutmayın **,\_hesap\_adı** ve **,\_hesap\_anahtar** toouse hesap adı ve hesap , sırasıyla anahtar.</span><span class="sxs-lookup"><span data-stu-id="19f06-172">Remember toomodify hello placeholder values **your\_account\_name** and **your\_account\_key** toouse your account name and account key, respectively.</span></span>

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

<span data-ttu-id="19f06-173">Toplama toouploading yerel görüntü dosyası tooAzure depolama hello örnek kod, tarayıcı toosee açabilirsiniz bir yerel dosya namedindex.html oluşturur, karşıya yüklenen görüntü.</span><span class="sxs-lookup"><span data-stu-id="19f06-173">In addition toouploading your local image file tooAzure storage, hello example code creates a local file namedindex.html, which you can open in your browser toosee your uploaded image.</span></span>

<span data-ttu-id="19f06-174">Merhaba kod hesap adı ve hesap anahtarını içerdiğinden, kaynak kodunuzu güvenli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="19f06-174">Because hello code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="toodelete-a-container"></a><span data-ttu-id="19f06-175">toodelete bir kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="19f06-175">toodelete a container</span></span>
<span data-ttu-id="19f06-176">Depolama için ücretlendirildiğinizden toodelete isteyebilirsiniz **gettingstarted** tamamladıktan sonra kapsayıcı ile bu örnek denemek.</span><span class="sxs-lookup"><span data-stu-id="19f06-176">Because you are charged for storage, you may want toodelete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="19f06-177">toodelete bir kapsayıcı kullanmak hello **CloudBlobContainer.delete** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="19f06-177">toodelete a container, use hello **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="19f06-178">toocall hello **CloudBlobContainer.delete** yöntemi, başlatma işleminin hello **CloudStorageAccount**, **ClodBlobClient**, ve  **CloudBlobContainer** nesneleri için gösterilen aynı hello olan **createIfNotExist** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="19f06-178">toocall hello **CloudBlobContainer.delete** method, hello process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is hello same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="19f06-179">Merhaba siler adlı kapsayıcı hello tam bir örnek verilmiştir **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="19f06-179">hello following is a complete example that deletes hello container named **gettingstarted**.</span></span>

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

<span data-ttu-id="19f06-180">Diğer blob depolama sınıflar ve yöntemler genel bakış için bkz: [nasıl toouse Java'dan Blob storage](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="19f06-180">For an overview of other blob storage classes and methods, see [How toouse Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="19f06-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19f06-181">Next steps</span></span>
<span data-ttu-id="19f06-182">Daha karmaşık depolama görevleri hakkında daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="19f06-182">Follow these links toolearn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="19f06-183">Azure depolama için Java SDK'sı</span><span class="sxs-lookup"><span data-stu-id="19f06-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="19f06-184">Azure Storage istemci SDK'sı başvurusu</span><span class="sxs-lookup"><span data-stu-id="19f06-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="19f06-185">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="19f06-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="19f06-186">Azure Depolama Ekibi Blog’u</span><span class="sxs-lookup"><span data-stu-id="19f06-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

