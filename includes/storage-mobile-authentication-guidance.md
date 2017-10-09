## <a name="configure-your-application-tooaccess-azure-storage"></a>Uygulama tooaccess Azure Storage yapılandırın
Depolama Hizmetleri, uygulama tooaccess iki yolu tooauthenticate vardır:

* Paylaşılan anahtar: Paylaşılan yalnızca test amacıyla anahtarı kullan
* Paylaşılan erişim imzası (SAS): Üretim uygulamaları SAS kullanılmak

### <a name="shared-key"></a>Paylaşılan Anahtar
Paylaşılan anahtar kimlik doğrulaması, uygulamanızın hesap adınızı kullanın ve depolama hizmetleri anahtar tooaccess hesap anlamına gelir. Hızlı bir şekilde gösteren hello amacıyla nasıl toouse bu kitaplığı Biz bu Başlarken, paylaşılan anahtar kimlik doğrulaması kullanır.

> [!WARNING] 
> **Yalnızca test amacıyla paylaşılan anahtar kimlik doğrulaması kullanın!** Hesap adı ve hesap anahtarı tam okuma/yazma erişimi toohello veren depolama hesabını ilişkili, uygulamanızı indirmeleri dağıtılmış tooevery kişi olacaktır. Bu **değil** güvenilmeyen istemciler tarafından tehlikeye anahtarınızı sahip risk gibi iyi bir uygulamadır.
> 
> 

Paylaşılan anahtar kimlik doğrulaması kullanırken, oluşturacağınız bir [bağlantı dizesi](../articles/storage/common/storage-configure-connection-string.md). Merhaba bağlantı dizesi oluşur:  

* Merhaba **DefaultEndpointsProtocol** -HTTP veya HTTPS seçebilirsiniz. Ancak, HTTPS kullanılması önerilir.
* Merhaba **hesap adı** - hello depolama hesabınızın adı
* Merhaba **hesap anahtarı** - hello [Azure Portal](https://portal.azure.com)tooyour depolama hesabına gidin ve hello tıklatın **anahtarları** simgesi toofind bu bilgileri.
* (İsteğe bağlı) **EndpointSuffix** -bu Azure Çin ya da Azure yönetimi gibi farklı uç nokta sonekleri ile bölgelerdeki depolama hizmetleri için kullanılır.

Burada, paylaşılan anahtar kimlik doğrulaması kullanarak bağlantı dizesi örneği verilmiştir:

`"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here"`

### <a name="shared-access-signatures-sas"></a>Paylaşılan Erişim İmzaları (SAS)
Bir mobil uygulama için bir paylaşılan erişim imzası (SAS) kullanarak hello Azure depolama hizmeti karşı bir istemci tarafından bir istek kimliğini doğrulamak için yöntem önerilen hello gerçekleşir. SAS bir belirtilen süre, belirtilen bir izin kümesi ile toogrant bir istemci erişim tooa kaynak sağlar.
Merhaba depolama hesabı sahibi, mobil istemcilerin tooconsume için toogenerate SAS gerekir. toogenerate SAS Merhaba, büyük olasılıkla toowrite hello SAS dağıtılmış toobe tooyour istemcileri oluşturur ayrı bir hizmet isteyeceksiniz. Test amacıyla, hello kullanabilirsiniz [Microsoft Azure Storage Gezgini](http://storageexplorer.com) veya hello [Azure Portal](https://portal.azure.com) toogenerate SAS. Hello SAS oluşturduğunuzda hello zaman aralığı hangi hello SAS geçerlidir ve SAS verir toohello istemci hello hello izinleri belirtebilirsiniz.

Aşağıdaki örnek hello nasıl toouse hello Microsoft Azure Storage Gezgini toogenerate SAS gösterir.

1. Henüz yapmadıysanız [yükleme hello Microsoft Azure Storage Gezgini](http://storageexplorer.com)
2. Tooyour abonelik bağlayın.
3. Depolama hesabınızdaki ve hello "Eylemler" sekmesinde hello altındaki sol tıklayın. "Paylaşılan erişim imzası Al" toogenerate "bağlantı dizesi" için SAS'ı tıklatın.
4. Burada, verir okuma ve yazma izinlerine hello hizmeti, kapsayıcı ve nesne düzeyinde hello hello depolama hesabının blob hizmeti için bir SAS bağlantı dizesi örneği verilmiştir.
   
   `"SharedAccessSignature=sv=2015-04-05&ss=b&srt=sco&sp=rw&se=2016-07-21T18%3A00%3A00Z&sig=3ABdLOJZosCp0o491T%2BqZGKIhafF1nlM3MzESDDD3Gg%3D;BlobEndpoint=https://youraccount.blob.core.windows.net"`

Bir SAS kullanırken görebileceğiniz gibi hesap anahtarınızı uygulamanızda gösterme değil. SAS ve SAS kullanıma kullanarak için en iyi uygulamalar hakkında daha fazla bilgiyi [paylaşılan erişim imzaları: hello SAS modelini anlama](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md).

