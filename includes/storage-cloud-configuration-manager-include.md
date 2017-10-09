Merhaba [.NET için Microsoft Azure Yapılandırma Yöneticisi Kitaplığı](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) yapılandırma dosyasından bağlantı dizesini ayrıştırmak için bir sınıf sağlar. Merhaba [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) sınıfı Merhaba istemci uygulaması hello masaüstünde, bir Azure sanal makinesi veya bir Azure bulut hizmeti bir mobil aygıtı kullanılıp kullanılmadığını bakılmaksızın yapılandırma ayarlarını ayrıştırır.

tooreference CloudConfigurationManager paketine Merhaba, hello aşağıdakileri ekleyin `using` yönergesi:

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

Aşağıda, nasıl tooretrieve bir bağlantı dizesi yapılandırma dosyasından gösteren bir örnek verilmiştir:

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

Hello Azure Yapılandırma Yöneticisi'ni kullanmak isteğe bağlıdır. .NET Framework'ün hello gibi bir API de kullanabilirsiniz [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) sınıfı.

