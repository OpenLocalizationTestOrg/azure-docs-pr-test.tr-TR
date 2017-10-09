<span data-ttu-id="fddb1-101">Merhaba [.NET için Microsoft Azure Yapılandırma Yöneticisi Kitaplığı](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) yapılandırma dosyasından bağlantı dizesini ayrıştırmak için bir sınıf sağlar.</span><span class="sxs-lookup"><span data-stu-id="fddb1-101">hello [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="fddb1-102">Merhaba [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) sınıfı Merhaba istemci uygulaması hello masaüstünde, bir Azure sanal makinesi veya bir Azure bulut hizmeti bir mobil aygıtı kullanılıp kullanılmadığını bakılmaksızın yapılandırma ayarlarını ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="fddb1-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether hello client application is running on hello desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="fddb1-103">tooreference CloudConfigurationManager paketine Merhaba, hello aşağıdakileri ekleyin `using` yönergesi:</span><span class="sxs-lookup"><span data-stu-id="fddb1-103">tooreference hello CloudConfigurationManager package, add hello following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="fddb1-104">Aşağıda, nasıl tooretrieve bir bağlantı dizesi yapılandırma dosyasından gösteren bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="fddb1-104">Here's an example that shows how tooretrieve a connection string from a configuration file:</span></span>

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="fddb1-105">Hello Azure Yapılandırma Yöneticisi'ni kullanmak isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fddb1-105">Using hello Azure Configuration Manager is optional.</span></span> <span data-ttu-id="fddb1-106">.NET Framework'ün hello gibi bir API de kullanabilirsiniz [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fddb1-106">You can also use an API like hello .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

