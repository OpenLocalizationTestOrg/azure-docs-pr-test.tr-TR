<span data-ttu-id="dc04f-101">Bir depolama hesabında tooresources erişiminizi bir paylaşılan erişim imzası (SAS) URL sahip bir bağlantı dizesi hello SAS kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc04f-101">If you possess a shared access signature (SAS) URL that grants you access tooresources in a storage account, you can use hello SAS in a connection string.</span></span> <span data-ttu-id="dc04f-102">Merhaba SAS hello bilgi gerekli tooauthenticate hello isteği içerdiğinden, SAS bağlantı dizesiyle hello protokolü, hello Hizmeti uç noktası ve hello gerekli kimlik bilgilerini tooaccess hello kaynak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dc04f-102">Because hello SAS contains hello information required tooauthenticate hello request, a connection string with a SAS provides hello protocol, hello service endpoint, and hello necessary credentials tooaccess hello resource.</span></span>

<span data-ttu-id="dc04f-103">toocreate bir paylaşılan erişim imzası içeren bir bağlantı dizesi biçimi aşağıdaki hello hello dizeyi belirtin:</span><span class="sxs-lookup"><span data-stu-id="dc04f-103">toocreate a connection string that includes a shared access signature, specify hello string in hello following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="dc04f-104">Her hizmet uç noktası isteğe bağlı olsa Hello bağlantı dizesi en az birini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="dc04f-104">Each service endpoint is optional, although hello connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="dc04f-105">HTTPS ile SAS kullanarak bir en iyi uygulama olarak önerilir.</span><span class="sxs-lookup"><span data-stu-id="dc04f-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="dc04f-106">Yapılandırma dosyasında bir bağlantı dizesi bir SAS belirtiyorsanız hello URL'de bulunan özel karakterleri tooencode gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="dc04f-106">If you are specifying a SAS in a connection string in a configuration file, you may need tooencode special characters in hello URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="dc04f-107">Hizmet SAS örneği</span><span class="sxs-lookup"><span data-stu-id="dc04f-107">Service SAS example</span></span>
<span data-ttu-id="dc04f-108">Burada, Blob storage için hizmet SAS içeren bir bağlantı dizesi örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="dc04f-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="dc04f-109">Burada da hello örneği özel karakter kodlama ile aynı bağlantı dizesi:</span><span class="sxs-lookup"><span data-stu-id="dc04f-109">And here's an example of hello same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="dc04f-110">Hesap SAS örneği</span><span class="sxs-lookup"><span data-stu-id="dc04f-110">Account SAS example</span></span>
<span data-ttu-id="dc04f-111">Burada, Blob ve dosya depolama için hesap SAS içeren bir bağlantı dizesi örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="dc04f-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="dc04f-112">Her iki hizmet için uç noktalar belirttiğiniz dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="dc04f-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="dc04f-113">Burada da hello örneği URL kodlaması ile aynı bağlantı dizesi:</span><span class="sxs-lookup"><span data-stu-id="dc04f-113">And here's an example of hello same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

