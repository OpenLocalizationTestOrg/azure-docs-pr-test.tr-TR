<span data-ttu-id="a3f8c-101">[.NET için Microsoft Azure Yapılandırma Yöneticisi Kitaplığı](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/), yapılandırma dosyasından bağlantı dizesini ayrıştırmak için bir sınıf sağlar.</span><span class="sxs-lookup"><span data-stu-id="a3f8c-101">The [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="a3f8c-102">[CloudConfigurationManager sınıfı](https://msdn.microsoft.com/library/azure/mt634650.aspx), Azure sanal cihazdaki veya Azure bulut hizmetindeki bir masaüstünde, bir mobil cihazda istemci uygulamasının çalışıp çalışmadığını göz ardı ederek yapılandırma ayarlarını ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="a3f8c-102">The [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether the client application is running on the desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="a3f8c-103">CloudConfigurationManager paketine başvurmak için şu `using` yönergeyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a3f8c-103">To reference the CloudConfigurationManager package, add the following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="a3f8c-104">Burada, yapılandırma dosyasından bir bağlantı dizesinin nasıl alındığını gösteren bir örnek bulunmaktadır:</span><span class="sxs-lookup"><span data-stu-id="a3f8c-104">Here's an example that shows how to retrieve a connection string from a configuration file:</span></span>

```csharp
// Parse the connection string and return a reference to the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="a3f8c-105">Azure Yapılandırma Yöneticisi'ni kullanmak isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a3f8c-105">Using the Azure Configuration Manager is optional.</span></span> <span data-ttu-id="a3f8c-106">.NET Framework'ün [ConfigurationManager sınıfı](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) gibi bir API de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3f8c-106">You can also use an API like the .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

