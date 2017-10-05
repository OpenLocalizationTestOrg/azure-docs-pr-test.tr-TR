---
title: "Hizmet parametreleri Azure veritabanı'nda PostgreSQL için yapılandırın. | Microsoft Docs"
description: "Bu makalede, Azure CLI komut satırını kullanarak PostgreSQL için Azure veritabanı'nda hizmet parametreleri yapılandırmak açıklar."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="b30f3-103">Azure CLI kullanarak sunucu yapılandırma parametreleri özelleştirme</span><span class="sxs-lookup"><span data-stu-id="b30f3-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="b30f3-104">Liste, Göster ve komut satırı arabirimi (Azure CLI) kullanarak bir Azure PostgreSQL sunucusu için yapılandırma parametrelerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b30f3-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="b30f3-105">Ancak, yalnızca bir alt kümesini altyapısı yapılandırmaları sunucu düzeyinde sunulur ve değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b30f3-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b30f3-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b30f3-106">Prerequisites</span></span>
<span data-ttu-id="b30f3-107">Nasıl yapılır bu kılavuzu adım için gerekir:</span><span class="sxs-lookup"><span data-stu-id="b30f3-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="b30f3-108">Sunucu ve veritabanına [PostgreSQL için bir Azure veritabanı oluşturma](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b30f3-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="b30f3-109">Yükleme [Azure CLI 2.0](/cli/azure/install-azure-cli) komut satırı yardımcı programı veya tarayıcıda Azure bulut Kabuğu'nu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b30f3-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="b30f3-110">Itanium tabanlı sistemler için liste sunucu yapılandırma parametreleri Azure veritabanı için PostgreSQL sunucusu</span><span class="sxs-lookup"><span data-stu-id="b30f3-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="b30f3-111">Tüm değiştirilebilir parametreler bir sunucu ve değerlerine listelemek için Çalıştır [az postgres sunucu yapılandırması listesi](/cli/azure/postgres/server/configuration#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="b30f3-111">To list all modifiable parameters in a server and their values, run the [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="b30f3-112">Sunucusu için sunucu yapılandırma parametrelerini listeleyebilirsiniz **mypgserver 20170401.postgres.database.azure.com** kaynak grubu altında **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="b30f3-112">You can list the server configuration parameters for the server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="b30f3-113">Sunucu yapılandırması parametre ayrıntıları göster</span><span class="sxs-lookup"><span data-stu-id="b30f3-113">Show server configuration parameter details</span></span>
<span data-ttu-id="b30f3-114">Bir sunucu için belirli yapılandırma parametresi hakkındaki ayrıntıları görüntülemek için Çalıştır [az postgres sunucu yapılandırması Göster](/cli/azure/postgres/server/configuration#show) komutu.</span><span class="sxs-lookup"><span data-stu-id="b30f3-114">To show details about a particular configuration parameter for a server, run the [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="b30f3-115">Bu örnek ayrıntılarını gösterir **günlük\_min\_iletileri** sunucusu için sunucu yapılandırma parametresi **mypgserver 20170401.postgres.database.azure.com** altında kaynak grubu **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="b30f3-115">This example shows details of the **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="b30f3-116">Sunucu Yapılandırma parametresi değerini değiştirin</span><span class="sxs-lookup"><span data-stu-id="b30f3-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="b30f3-117">Belirli bir sunucu yapılandırma parametresinin değerini de değiştirebilirsiniz ve bu PostgreSQL sunucu altyapısı için temel yapılandırma değeri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b30f3-117">You can also modify the value of a certain server configuration parameter, and this updates the underlying configuration value for the PostgreSQL server engine.</span></span> <span data-ttu-id="b30f3-118">Yapılandırma kullanımı güncelleştirmek için [az postgres sunucu yapılandırma kümesi](/cli/azure/postgres/server/configuration#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="b30f3-118">To update the configuration use the [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="b30f3-119">Güncelleştirilecek **günlük\_min\_iletileri** sunucu yapılandırma parametresi sunucunun **mypgserver 20170401.postgres.database.azure.com** kaynakgrubundaki**myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="b30f3-119">To update the **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="b30f3-120">Bir yapılandırma parametresinin değerini sıfırlamak istiyorsanız, yalnızca isteğe bağlı olarak bırakmak seçtiğiniz `--value` parametre ve hizmeti varsayılan değer uygulanacaktır.</span><span class="sxs-lookup"><span data-stu-id="b30f3-120">If you want to reset the value of a configuration parameter, you simply choose to leave out the optional `--value` parameter, and the service will apply the default value.</span></span> <span data-ttu-id="b30f3-121">İçinde Yukarıdaki örnek, onu gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="b30f3-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="b30f3-122">Bu sıfırlanacak **günlük\_min\_iletileri** varsayılan değere yapılandırma **uyarı**.</span><span class="sxs-lookup"><span data-stu-id="b30f3-122">This will reset the **log\_min\_messages** configuration to the default value **WARNING**.</span></span> <span data-ttu-id="b30f3-123">Sunucu Yapılandırması ve izin verilen değerlere daha ayrıntılı bilgi için üzerinde PostgreSQL belgelerine bakın. [sunucu yapılandırması](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="b30f3-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b30f3-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b30f3-124">Next steps</span></span>
- <span data-ttu-id="b30f3-125">Yapılandırma ve sunucu günlüklerini erişmek için bkz: [PostgreSQL için Azure veritabanında sunucu günlükleri](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="b30f3-125">To configure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
