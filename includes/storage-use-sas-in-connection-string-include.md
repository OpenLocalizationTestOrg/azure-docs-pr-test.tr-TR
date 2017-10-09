Bir depolama hesabında tooresources erişiminizi bir paylaşılan erişim imzası (SAS) URL sahip bir bağlantı dizesi hello SAS kullanabilirsiniz. Merhaba SAS hello bilgi gerekli tooauthenticate hello isteği içerdiğinden, SAS bağlantı dizesiyle hello protokolü, hello Hizmeti uç noktası ve hello gerekli kimlik bilgilerini tooaccess hello kaynak sağlar.

toocreate bir paylaşılan erişim imzası içeren bir bağlantı dizesi biçimi aşağıdaki hello hello dizeyi belirtin:

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

Her hizmet uç noktası isteğe bağlı olsa Hello bağlantı dizesi en az birini içermelidir.

> [!NOTE]
> HTTPS ile SAS kullanarak bir en iyi uygulama olarak önerilir.
>
> Yapılandırma dosyasında bir bağlantı dizesi bir SAS belirtiyorsanız hello URL'de bulunan özel karakterleri tooencode gerekebilir.
>
>

### <a name="service-sas-example"></a>Hizmet SAS örneği
Burada, Blob storage için hizmet SAS içeren bir bağlantı dizesi örneği verilmiştir:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

Burada da hello örneği özel karakter kodlama ile aynı bağlantı dizesi:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a>Hesap SAS örneği
Burada, Blob ve dosya depolama için hesap SAS içeren bir bağlantı dizesi örneği verilmiştir. Her iki hizmet için uç noktalar belirttiğiniz dikkat edin:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

Burada da hello örneği URL kodlaması ile aynı bağlantı dizesi:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

