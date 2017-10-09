Merhaba depolama öykünücüsü paylaşılan anahtar kimlik doğrulaması için tek bir sabit hesap ve bilinen bir kimlik doğrulama anahtarı destekler. Bu hesabı ve anahtarı hello depolama öykünücüsü ile kullanmak için izin verilen hello yalnızca paylaşılan anahtar kimlik bilgileridir. Bunlar:

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> Merhaba depolama öykünücüsü tarafından desteklenen hello kimlik doğrulama anahtarı yalnızca sınama hello işlevselliğini istemci kimlik doğrulama kodunuzu için tasarlanmıştır. Herhangi bir güvenlik amaçla sunmuyor. Üretim depolama hesabı ve anahtarı hello depolama öykünücü ile kullanamazsınız. Üretim verileri ile Merhaba geliştirme hesap kullanmamalısınız.
> 
> Merhaba depolama öykünücüsü yalnızca bağlantı HTTP üzerinden destekler. Ancak, HTTPS protokolü üretimde Azure depolama hesabı kaynaklarına erişim için önerilen hello ' dir.
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>Toohello öykünücüsü hesabını kısayolunu kullanarak bağlan
Merhaba en kolay yolu tooconnect toohello depolama öykünücüsünün uygulamanızdan olduğundan tooconfigure hello kısayol başvuruyor, uygulamanızın yapılandırma dosyasındaki bağlantı dizesi `UseDevelopmentStorage=true`. Bir bağlantı dizesi toohello depolama öykünücüsünde bir örneği burada verilmiştir bir *app.config* dosyası: 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>Toohello öykünücüsü hesap Hello iyi bilinen hesap adı ve anahtarı kullanarak bağlan
toocreate başvuruları öykünücüsü hesap adı hello ve her hello Hizmetleri için anahtar, hello uç noktaları belirtmeniz gerekir bir bağlantı dizesi hello öykücüsünden hello bağlantı dizesinde toouse istiyor. Merhaba bağlantı dizesi bir üretim depolama hesabı için farklı hello öykünücüsü uç başvurur böylece, bu gereklidir. Örneğin, bağlantı dizenizi hello değerini şuna benzeyecektir:

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

Bu değer, yukarıda gösterilen aynı toohello kısayoludur `UseDevelopmentStorage=true`.

#### <a name="specify-an-http-proxy"></a>Bir HTTP Ara sunucusunu belirtin
Hizmetinizi hello storage öykünücüsüne karşı sınarken bir HTTP proxy toouse de belirtebilirsiniz. Bu işlemleri hello depolama hizmetleri karşı hatalarını ayıkladığınız sırada HTTP istekleri ve yanıtları Gözlemleme için yararlı olabilir. toospecify bir proxy eklemek hello `DevelopmentStorageProxyUri` seçeneği toohello bağlantı dizesini ve onun değeri toohello proxy URI ayarlayın. Örneğin, toohello depolama öykünücüsü işaret eder ve bir HTTP proxy yapılandıran bir bağlantı dizesi şöyledir:

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

