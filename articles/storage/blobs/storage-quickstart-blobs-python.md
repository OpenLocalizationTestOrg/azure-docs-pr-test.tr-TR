---
title: "Azure Hızlı Başlangıç - Python kullanarak nesneleri Azure Blob depolama içine/dışına aktarma | Microsoft Docs"
description: "Python kullanarak nesneleri Azure Blob depolama içine/dışına aktarmayı kısa sürede öğrenin"
services: storage
author: ruthogunnnaike
manager: jeconnoc
ms.service: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: quickstart
ms.date: 10/12/2017
ms.author: v-ruogun
ms.openlocfilehash: 50f43e6ef9ee60cbf489bb8d0c1c64ca61a393e1
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/02/2018
---
#  <a name="transfer-objects-tofrom-azure-blob-storage-using-python"></a>Python kullanarak nesneleri Azure Blob depolama içine/dışına aktarma
Bu hızlı başlangıçta, Azure Blob depolamadaki bir kapsayıcıda blok bloblarını karşıya yüklemek, indirmek ve listelemek için Python’ı nasıl kullanabileceğinizi öğreneceksiniz. 

## <a name="prerequisites"></a>Ön koşullar

Bu hızlı başlangıcı tamamlamak için: 
* [Python](https://www.python.org/downloads/)’ı yükleyin
* [Python için Azure Depolama SDK](storage-python-how-to-use-blob-storage.md#download-and-install-azure-storage-sdk-for-python)’yı indirin ve yükleyin. 

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [storage-quickstart-tutorial-create-account-portal](../../../includes/storage-quickstart-tutorial-create-account-portal.md)]

## <a name="download-the-sample-application"></a>Örnek uygulamayı indirin:
Bu [hızlı başlangıçta](https://github.com/Azure-Samples/storage-blobs-python-quickstart.git) kullanılan örnek uygulama, temel bir Python uygulamasıdır.  

Uygulamanın bir kopyasını geliştirme ortamınıza indirmek için [Git](https://git-scm.com/)’i kullanın. 

```bash
git clone https://github.com/Azure-Samples/storage-blobs-python-quickstart.git 
```

Bu komut, depoyu yerel Git klasörünüze kopyalar. Python programını açmak için, storage-blobs-python-quickstart klasörünü ve example.py dosyasını açın.  

## <a name="configure-your-storage-connection-string"></a>Depolama bağlantı dizelerinizi yapılandırma
Uygulamada, `BlockBlobService` nesnesi oluşturmak için depolama hesabı adınızı ve hesap anahtarınızı sağlamanız gerekir. IDE’nizdeki Çözüm Gezgini'nde `example.py` dosyasını açın. **accountname** ve **accountkey** değerlerini, hesap adınız ve anahtarınızla değiştirin. 

```python 
block_blob_service = BlockBlobService(account_name='accountname', account_key='accountkey') 
```

## <a name="run-the-sample"></a>Örneği çalıştırma
Bu örnek, 'Belgeler' klasöründe bir sınama dosyası oluşturur. Örnek program sınama dosyasını Blob depolamaya yükler, kapsayıcıdaki blobları listeler ve dosyayı yeni bir adla indirir. 

Örnek uygulamayı çalıştırın. Aşağıdaki çıktı, uygulama çalıştırılırken döndürülen çıktının bir örneğidir:
  
```
Temp file = C:\Users\azureuser\Documents\QuickStart_9f4ed0f9-22d3-43e1-98d0-8b2c05c01078.txt

Uploading to Blob storage as blobQuickStart_9f4ed0f9-22d3-43e1-98d0-8b2c05c01078.txt

List blobs in the container
         Blob name: QuickStart_9f4ed0f9-22d3-43e1-98d0-8b2c05c01078.txt

Downloading blob to C:\Users\azureuser\Documents\QuickStart_9f4ed0f9-22d3-43e1-98d0-8b2c05c01078_DOWNLOADED.txt
```
Devam etmek için herhangi bir tuşa bastığınızda, örnek program depolama kapsayıcısını ve dosyaları siler. Devam etmeden önce, iki dosya için 'Belgeler' klasörünüzü kontrol edin. Dosyaları açarak aynı olduklarını görebilirsiniz.

Ayrıca, Blob depolamadaki dosyaları görüntülemek için, [Azure Depolama Gezgini](http://storageexplorer.com) gibi bir araç da kullanabilirsiniz. Azure Depolama Gezgini, depolama hesabı bilgilerinize erişmenize olanak tanıyan ücretsiz ve platformlar arası bir araçtır. 

Dosyaları doğruladıktan sonra, tanıtımı tamamlamak ve test dosyalarını silmek için herhangi bir tuşa basın. Artık örnek dosyanın işlevini gördüğünüze göre, koda göz atmak için example.py dosyasını açabilirsiniz. 

## <a name="understand-the-sample-code"></a>Örnek kodu anlama

Sonraki aşamada, nasıl çalıştığını anlayabilmeniz için örnek kodu inceleyeceğiz.

### <a name="get-references-to-the-storage-objects"></a>Depolama nesneleriyle ilgili başvuruları alma
İlk önce, Blob depolamaya erişmek ve Blob depolamayı yönetmek için kullanılan nesnelere başvuru oluşturmaktır. Bu nesneler birbirleri üzerinde derlenir ve her bir dosya, listede yanında yer alan dosya tarafından kullanılır.

* Depolama hesabınızdaki Blob hizmetine işaret eden bir **BlobService** nesne örneği oluşturun. 

* Eriştiğiniz kapsayıcıyı ifade eden bir **CloudBlobContainer** nesne örneği oluşturun. Kapsayıcılar, tıpkı bilgisayarınızdaki dosyaları düzenlemek için klasörleri kullandığınız gibi blobları düzenlemek için kullanılır.

Bulut Blob kapsayıcısına sahip olduğunuzda, dilediğiniz bloba işaret eden **CloudBlockBlob** nesne örneği oluşturabilir ve karşıya yükleme, indirme ve kopyalama işlemleri gerçekleştirebilirsiniz.

> [!IMPORTANT]
> Kapsayıcı adlarının küçük harfle yazılması gerekir. Kapsayıcılar ve blob adları hakkında daha fazla bilgi için bkz. [Kapsayıcıları, Blobları ve Meta Verileri Adlandırma ve Bunlara Başvurma](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata).

Bu bölümde nesne örneği ve yeni bir kapsayıcı oluşturacak ve ardından kapsayıcıdaki izinleri bloblar herkese açık olacak şekilde ayarlayacaksınız. Bu kapsayıcının adı **quickstartblobs**’dur. 

```python 
# Create the BlockBlockService that is used to call the Blob service for the storage account
block_blob_service = BlockBlobService(account_name='accountname', account_key='accountkey') 
 
# Create a container called 'quickstartblobs'.
container_name ='quickstartblobs'
block_blob_service.create_container(container_name) 

# Set the permission so the blobs are public.
block_blob_service.set_container_acl(container_name, public_access=PublicAccess.Container)
```
### <a name="upload-blobs-to-the-container"></a>Blobları kapsayıcıya yükleme

Blob depolama blok blobları, ekleme bloblarını ve sayfa bloblarını destekler. Blok blobları en sık kullanılan bloblardır ve bu hızlı başlangıçta bu bloblar kullanılmıştır.  

Bir dosyayı bloba yüklemek için, yerel diskinizdeki dizin adıyla dosya adını birleştirerek dosyanın tam yolunu alın. Sonra, dosyayı belirtilen yola **create\_blob\_from\_path** metoduyla yükleyebilirsiniz. 

Örnek kod, karşıya yükleme ve indirme için kullanılacak yerel bir dosya oluşturur, karşıya yüklenecek dosyayı **file\_path\_to\_file** olarak ve blob adını **local\_file\_name** olarak depolar. Aşağıdaki örnek, dosyayı **quickstartblobs** adlı kapsayıcınıza yükler.

```python
# Create a file in Documents to test the upload and download.
local_path=os.path.expanduser("~\Documents")
local_file_name ="QuickStart_" + str(uuid.uuid4()) + ".txt"
full_path_to_file =os.path.join(local_path, local_file_name)

# Write text to the file.
file = open(full_path_to_file,  'w')
file.write("Hello, World!")
file.close()

print("Temp file = " + full_path_to_file)
print("\nUploading to Blob storage as blob" + local_file_name)

# Upload the created file, use local_file_name for the blob name
block_blob_service.create_blob_from_path(container_name, local_file_name, full_path_to_file)
```

Blob depolamayla kullanabileceğiniz çeşitli karşıya yükleme yöntemleri vardır. Örneğin, bellek akışınız varsa **create\_blob\_from\_path**. yerine **create\_blob\_from\_stream** metodunu kullanabilirsiniz. 

Blok bloblarının boyutu 4,7 TB’yi bulabilir ve bu bloblar Excel elektronik tablolarından büyük video dosyalarına kadar birçok türde olabilir. Sayfa blobları öncelikli olarak IaaS VM'leri desteklemek için kullanılan VHD dosyalarında kullanılır. Ekleme blobları, bir dosyaya yazıp daha sonradan daha fazla bilgi eklemek istediğiniz durumlarda günlüğe kaydetme için kullanılır. Blob depolamada depolanan nesnelerin çoğu blok blobudur.

### <a name="list-the-blobs-in-a-container"></a>Blob’ları bir kapsayıcıda listeleme

**list_blobs** metodunu kullanarak kapsayıcıdaki dosya listesini alın. Bu yöntem bir oluşturucu döndürür. Aşağıdaki kod blob listesini alır, ardından bu bloblarda döngü yapar ve kapsayıcıda bulunan blobların adlarını gösterir.  

```python
# List the blobs in the container
print("\nList blobs in the container")
    generator = block_blob_service.list_blobs(container_name)
    for blob in generator:
        print("\t Blob name: " + blob.name)
```

### <a name="download-the-blobs"></a>Blobları indirme

**get\_blob\_to\_path** metodunu kullanarak blobları yerel diskinize indirin. Aşağıdaki kod, önceki bir bölüme yüklenen blobu indirir. Yerel diskte yer alan iki dosyayı da görebilmeniz için, blob adının sonuna "_DOWNLOADED" son eki getirilir. 

```python
# Download the blob(s).
# Add '_DOWNLOADED' as prefix to '.txt' so you can see both files in Documents.
full_path_to_file2 = os.path.join(local_path, string.replace(local_file_name ,'.txt', '_DOWNLOADED.txt'))
print("\nDownloading blob to " + full_path_to_file2)
block_blob_service.get_blob_to_path(container_name, local_file_name, full_path_to_file2)
```

### <a name="clean-up-resources"></a>Kaynakları temizleme
Bu hızlı başlangıçta karşıya yüklenen bloblara artık ihtiyacınız kalmadığında, **delete\_container** kullanarak kapsayıcının tamamını silebilirsiniz. Oluşturulan dosyalara artık ihtiyaç duymuyorsanız dosyaları silmek için **delete\_blob** metodunu kullanırsınız.

```python
# Clean up resources. This includes the container and the temp files
block_blob_service.delete_container(container_name)
os.remove(full_path_to_file)
os.remove(full_path_to_file2)
```

## <a name="next-steps"></a>Sonraki adımlar
 
Bu hızlı başlangıçta, dosyaları Python kullanarak yerel bir disk ve Azure blob depolama arasında aktarmayı öğrendiniz. Blob depolamayla çalışma hakkında daha fazla bilgi edinmek için, Blob depolama nasıl yapılır öğreticisiyle devam edin.

> [!div class="nextstepaction"]
> [Blob Depolama İşlemleri Nasıl Yapılır](./storage-python-how-to-use-blob-storage.md)
 

Depolama Gezgini ve Bloblar hakkında daha fazla bilgi için bkz. [Azure Blob depolama kaynaklarını Depolama Gezgini'yle yönetme](../../vs-azure-tools-storage-explorer-blobs.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).
