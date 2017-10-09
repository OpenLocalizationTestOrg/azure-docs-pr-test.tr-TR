## <a name="set-up-your-development-environment"></a>Geliştirme ortamınızı kurma
Ardından, bu kılavuzdaki hazır tootry hello kod örnekleri olacak şekilde geliştirme ortamınızı Visual Studio'da ayarlayın.

### <a name="create-a-windows-console-application-project"></a>Windows konsol uygulaması projesi oluşturma
Visual Studio'da yeni bir Windows konsol uygulaması oluşturun. Aşağıdaki adımları hello nasıl toocreate bir konsol uygulaması Visual Studio 2017, ancak başlangıç adımları benzerdir diğer Visual Studio sürümlerinde gösterir.

1. **Dosya** > **Yeni** > **Proje**’yi seçin
2. **Yüklü** > **Şablonlar** > **Visual C#** > **Windows Klasik Masaüstü** öğesini seçin
3. **Konsol Uygulaması (.NET Framework)** öğesini seçin
4. Hello uygulamanız için bir ad girin **Name:** alanı
5. **Tamam**’ı seçin

![Visual Studio'da proje oluşturma iletişim kutusu](./media/storage-development-environment-include/storage-development-environment-include-1.png)

Bu öğreticideki tüm kod örnekleri toohello eklenebilir `Main()` konsol uygulamanızın yöntemi `Program.cs` dosya.

Herhangi bir Azure bulut hizmeti veya web uygulaması dahil olmak üzere, .NET uygulaması ve Masaüstü ve mobil uygulamaları türünde hello Azure Storage istemci kitaplığı kullanabilirsiniz. Bu kılavuzda, sadeleştirmek için konsol uygulaması kullanmaktayız.

### <a name="use-nuget-tooinstall-hello-required-packages"></a>NuGet tooinstall gerekli hello paketlerini kullanma
Bu öğretici, proje toocomplete tooreference gereken iki paket vardır:

* [.NET için Microsoft Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/): Bu paket depolama hesabınızdaki toodata kaynaklara programlı erişim sağlar.
* [.NET için Microsoft Azure Configuration Manager Kitaplığı](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): Bu paket, uygulamanızın nerede çalıştığına bakmaksızın yapılandırma dosyasından bağlantı dizesini ayrıştırmak için bir sınıf sağlar.

Her iki paket NuGet tooobtain kullanabilirsiniz. Şu adımları uygulayın:

1. **Çözüm Gezgini**'nde projenize sağ tıklayın ve **NuGet Paketlerini Yönet**’i seçin.
2. Çevrimiçi olarak "WindowsAzure.Storage" ifadesini arayın ve'ı tıklatın **yükleme** tooinstall hello depolama istemci kitaplığı ve bağımlılıklarını.
3. Çevrimiçi "WindowsAzure.ConfigurationManager" için arama ve tıklayın **yükleme** tooinstall hello Azure Yapılandırma Yöneticisi.

> [!NOTE]
> Merhaba depolama istemcisi kitaplığı paketi hello de dahil [.NET için Azure SDK](https://azure.microsoft.com/downloads/). Ancak, hello depolama istemci kitaplığı ayrıca her zaman en son sürümünü hello istemci kitaplığı hello sahip NuGet tooensure yüklemenizi öneririz.
> 
> Merhaba .NET için depolama istemci kitaplığı Hello ODataLib bağımlılıkları, WCF Veri Hizmetleri değil, NuGet üzerinde kullanılabilir hello ODataLib paketleri tarafından çözümlenir. Merhaba ODataLib kitaplıkları doğrudan indirilebilir veya kod projenizle NuGet aracılığıyla başvurulan. Merhaba Hello depolama istemci kitaplığı tarafından kullanılan belirli ODataLib paketleri [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), ve [Spatial](http://nuget.org/packages/System.Spatial/). Bu kitaplıklar hello Azure Table storage sınıfları tarafından kullanılırken, hello depolama istemci Kitaplığı'yla programlama için gerekli bağımlılıkları oldukları.
> 
> 

### <a name="determine-your-target-environment"></a>Hedef ortamınızı saptama
Bu kılavuzda hello örnekleri çalıştırmak için iki ortam seçeneğiniz vardır:

* Kodunuzu hello buluttaki bir Azure Storage hesabını karşı çalıştırabilirsiniz. 
* Kodunuzu hello Azure storage öykünücüsüne karşı çalıştırabilirsiniz. Merhaba depolama öykünücüsü hello buluttaki bir Azure Storage hesabını öykünen bir yerel ortamdır. Merhaba öykünücüsü, test ve uygulamanız geliştirildiği sırada kodunuzu hata ayıklama için boş bir seçenektir. Merhaba öykünücü iyi bilinen hesabı ve anahtarı kullanır. Daha fazla bilgi için bkz: [kullanım hello geliştirme ve sınama için Azure Storage öykünücüsü](../articles/storage/common/storage-use-emulator.md)

Merhaba buluttaki bir depolama hesabını hedefliyorsanız, depolama hesabınız için birincil erişim anahtarını hello hello Azure portal ' kopyalayın. Daha fazla bilgi için bkz. [Depolama erişim anahtarlarını görüntüleme ve kopyalama](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).

> [!NOTE]
> Azure Storage ile ilişkili maliyetlerin oluşmasını hello depolama öykünücüsü tooavoid hedefleyebilirsiniz. Ancak, bir Azure depolama hesabı tootarget hello bulutta seçerseniz, bu öğreticiyi gerçekleştirme maliyetleri göz ardı edilecektir.
> 
> 

### <a name="configure-your-storage-connection-string"></a>Depolama bağlantı dizelerinizi yapılandırma
Hello .NET için Azure Storage istemci kitaplığı, bir depolama bağlantı dizesi tooconfigure uç noktalarını kullanarak destekler ve depolama hizmetleri erişmek için kimlik bilgileri. Merhaba en iyi şekilde toomaintain depolama bağlantı dizenizi bir yapılandırma dosyasında ' dir. 

Bağlantı dizeleri hakkında daha fazla bilgi için bkz: [bir bağlantı dizesi tooAzure depolama yapılandırma](../articles/storage/common/storage-configure-connection-string.md).

> [!NOTE]
> Depolama hesabı anahtarınız depolama hesabınız için benzer toohello kök parola değil. Her zaman dikkatli tooprotect depolama hesabı anahtarınızı olabilir. Sabit kodlama veya erişilebilir tooothers olan bir düz metin dosyasına kaydetme tooother kullanıcılar dağıtma kaçının. Bunu tehlikede olduğunu düşünüyorsanız, hello Azure portalı kullanarak hesap anahtarınızı yeniden oluşturun.
> 
> 

tooconfigure bağlantı dizesi, açık hello `app.config` Visual Studio'daki Çözüm Gezgini'nden dosya. Merhaba Merhaba içeriğine Ekle `<appSettings>` aşağıda gösterilen öğesi. Değiştir `account-name` depolama hesabınızın hello adla ve `account-key` hesap erişim anahtarı ile:

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

Örneğin, yapılandırma ayarınız şunun gibi görünür:

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

tootarget hello depolama öykünücüsü, toohello iyi bilinen hesap adı ve anahtar eşleşen bir kısayolu kullanabilirsiniz. Bu durumda, bağlantı dizesi ayarı şöyle olur:

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

