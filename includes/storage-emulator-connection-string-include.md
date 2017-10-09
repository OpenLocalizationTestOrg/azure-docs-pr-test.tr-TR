<span data-ttu-id="a3325-101">Merhaba depolama öykünücüsü paylaşılan anahtar kimlik doğrulaması için tek bir sabit hesap ve bilinen bir kimlik doğrulama anahtarı destekler.</span><span class="sxs-lookup"><span data-stu-id="a3325-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="a3325-102">Bu hesabı ve anahtarı hello depolama öykünücüsü ile kullanmak için izin verilen hello yalnızca paylaşılan anahtar kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="a3325-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="a3325-103">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="a3325-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="a3325-104">Merhaba depolama öykünücüsü tarafından desteklenen hello kimlik doğrulama anahtarı yalnızca sınama hello işlevselliğini istemci kimlik doğrulama kodunuzu için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a3325-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="a3325-105">Herhangi bir güvenlik amaçla sunmuyor.</span><span class="sxs-lookup"><span data-stu-id="a3325-105">It does not serve any security purpose.</span></span> <span data-ttu-id="a3325-106">Üretim depolama hesabı ve anahtarı hello depolama öykünücü ile kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="a3325-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="a3325-107">Üretim verileri ile Merhaba geliştirme hesap kullanmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="a3325-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="a3325-108">Merhaba depolama öykünücüsü yalnızca bağlantı HTTP üzerinden destekler.</span><span class="sxs-lookup"><span data-stu-id="a3325-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="a3325-109">Ancak, HTTPS protokolü üretimde Azure depolama hesabı kaynaklarına erişim için önerilen hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="a3325-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="a3325-110">Toohello öykünücüsü hesabını kısayolunu kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="a3325-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="a3325-111">Merhaba en kolay yolu tooconnect toohello depolama öykünücüsünün uygulamanızdan olduğundan tooconfigure hello kısayol başvuruyor, uygulamanızın yapılandırma dosyasındaki bağlantı dizesi `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="a3325-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="a3325-112">Bir bağlantı dizesi toohello depolama öykünücüsünde bir örneği burada verilmiştir bir *app.config* dosyası:</span><span class="sxs-lookup"><span data-stu-id="a3325-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="a3325-113">Toohello öykünücüsü hesap Hello iyi bilinen hesap adı ve anahtarı kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="a3325-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="a3325-114">toocreate başvuruları öykünücüsü hesap adı hello ve her hello Hizmetleri için anahtar, hello uç noktaları belirtmeniz gerekir bir bağlantı dizesi hello öykücüsünden hello bağlantı dizesinde toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="a3325-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="a3325-115">Merhaba bağlantı dizesi bir üretim depolama hesabı için farklı hello öykünücüsü uç başvurur böylece, bu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a3325-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="a3325-116">Örneğin, bağlantı dizenizi hello değerini şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="a3325-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="a3325-117">Bu değer, yukarıda gösterilen aynı toohello kısayoludur `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="a3325-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="a3325-118">Bir HTTP Ara sunucusunu belirtin</span><span class="sxs-lookup"><span data-stu-id="a3325-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="a3325-119">Hizmetinizi hello storage öykünücüsüne karşı sınarken bir HTTP proxy toouse de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3325-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="a3325-120">Bu işlemleri hello depolama hizmetleri karşı hatalarını ayıkladığınız sırada HTTP istekleri ve yanıtları Gözlemleme için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a3325-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="a3325-121">toospecify bir proxy eklemek hello `DevelopmentStorageProxyUri` seçeneği toohello bağlantı dizesini ve onun değeri toohello proxy URI ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a3325-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="a3325-122">Örneğin, toohello depolama öykünücüsü işaret eder ve bir HTTP proxy yapılandıran bir bağlantı dizesi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a3325-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

