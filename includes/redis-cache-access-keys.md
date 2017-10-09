tooconnect tooan Azure Redis önbelleği örneği, önbellek istemcilerinin hello ana bilgisayar adı, bağlantı noktalarını ve anahtarları hello önbelleğin gerekir. Bazı istemciler toothese öğeleri biraz daha farklı adlarla başvurabilir. Bu bilgi hello Azure portalında veya Azure CLI gibi komut satırı araçlarını kullanarak alabilirsiniz.

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>Ana bilgisayar adı, bağlantı noktalarını ve hello Azure Portal kullanarak erişim anahtarlarını alma
tooretrieve ana bilgisayar adı, bağlantı noktalarını ve erişim anahtarlarını hello Azure Portal kullanarak [Gözat](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) hello tooyour önbellekte [Azure portal](https://portal.azure.com) tıklatıp **erişim anahtarları** ve  **Özellikler** hello içinde **kaynak menü**. 

![Redis Cache ayarları](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>Azure CLI kullanarak ana bilgisayar adı, bağlantı noktaları ve erişim anahtarlarını alma
tooretrieve hello ana bilgisayar adı ve bağlantı noktaları Azure CLI 2.0 kullanan çağırabilirsiniz [az redis Göster](https://docs.microsoft.com/cli/azure/redis#show)ve çağırabilirsiniz tooretrieve hello anahtarları [az redis listesi anahtarları](https://docs.microsoft.com/cli/azure/redis#list-keys). Merhaba aşağıdaki komut dosyasını çağıran şu iki komutu ve ana bilgisayar adı, bağlantı noktalarını ve anahtarları toohello konsol kırmak hello.

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

Bu komut hakkında daha fazla bilgi için bkz: [Azure Redis önbelleği için hello ana bilgisayar adı, bağlantı noktalarını ve anahtarları alma](../articles/redis-cache/scripts/cache-keys-ports.md). Azure CLI 2.0 hakkında daha fazla bilgi için bkz. [Azure CLI 2.0 yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli) ve [Azure CLI 2.0 ile çalışmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).
