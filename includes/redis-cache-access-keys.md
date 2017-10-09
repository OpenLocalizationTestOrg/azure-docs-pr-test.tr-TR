<span data-ttu-id="53f5c-101">tooconnect tooan Azure Redis önbelleği örneği, önbellek istemcilerinin hello ana bilgisayar adı, bağlantı noktalarını ve anahtarları hello önbelleğin gerekir.</span><span class="sxs-lookup"><span data-stu-id="53f5c-101">tooconnect tooan Azure Redis Cache instance, cache clients need hello host name, ports, and keys of hello cache.</span></span> <span data-ttu-id="53f5c-102">Bazı istemciler toothese öğeleri biraz daha farklı adlarla başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="53f5c-102">Some clients may refer toothese items by slightly different names.</span></span> <span data-ttu-id="53f5c-103">Bu bilgi hello Azure portalında veya Azure CLI gibi komut satırı araçlarını kullanarak alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53f5c-103">You can retrieve this information in hello Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a><span data-ttu-id="53f5c-104">Ana bilgisayar adı, bağlantı noktalarını ve hello Azure Portal kullanarak erişim anahtarlarını alma</span><span class="sxs-lookup"><span data-stu-id="53f5c-104">Retrieve host name, ports, and access keys using hello Azure Portal</span></span>
<span data-ttu-id="53f5c-105">tooretrieve ana bilgisayar adı, bağlantı noktalarını ve erişim anahtarlarını hello Azure Portal kullanarak [Gözat](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) hello tooyour önbellekte [Azure portal](https://portal.azure.com) tıklatıp **erişim anahtarları** ve  **Özellikler** hello içinde **kaynak menü**.</span><span class="sxs-lookup"><span data-stu-id="53f5c-105">tooretrieve host name, ports, and access keys using hello Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in hello [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in hello **Resource menu**.</span></span> 

![Redis Cache ayarları](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="53f5c-107">Azure CLI kullanarak ana bilgisayar adı, bağlantı noktaları ve erişim anahtarlarını alma</span><span class="sxs-lookup"><span data-stu-id="53f5c-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="53f5c-108">tooretrieve hello ana bilgisayar adı ve bağlantı noktaları Azure CLI 2.0 kullanan çağırabilirsiniz [az redis Göster](https://docs.microsoft.com/cli/azure/redis#show)ve çağırabilirsiniz tooretrieve hello anahtarları [az redis listesi anahtarları](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="53f5c-108">tooretrieve hello host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and tooretrieve hello keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="53f5c-109">Merhaba aşağıdaki komut dosyasını çağıran şu iki komutu ve ana bilgisayar adı, bağlantı noktalarını ve anahtarları toohello konsol kırmak hello.</span><span class="sxs-lookup"><span data-stu-id="53f5c-109">hello following script calls these two commands and echos hello hostname, ports, and keys toohello console.</span></span>

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

<span data-ttu-id="53f5c-110">Bu komut hakkında daha fazla bilgi için bkz: [Azure Redis önbelleği için hello ana bilgisayar adı, bağlantı noktalarını ve anahtarları alma](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="53f5c-110">For more information about this script, see [Get hello hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="53f5c-111">Azure CLI 2.0 hakkında daha fazla bilgi için bkz. [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli) ve [Azure CLI 2.0 ile çalışmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="53f5c-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
