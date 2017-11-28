---
title: "aaaConfigure hello hizmeti parametreleri PostgreSQL için Azure veritabanında | Microsoft Docs"
description: "Bu makalede, Azure CLI komut satırı PostgreSQL kullanma tooconfigure hello hizmeti parametreleri Azure veritabanında nasıl hello açıklanmaktadır."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="69b97-103">Azure CLI kullanarak sunucu yapılandırma parametreleri özelleştirme</span><span class="sxs-lookup"><span data-stu-id="69b97-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="69b97-104">Liste, Göster ve hello komut satırı arabirimi (Azure CLI) kullanarak bir Azure PostgreSQL sunucusu için yapılandırma parametrelerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="69b97-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="69b97-105">Ancak, yalnızca bir alt kümesini altyapısı yapılandırmaları sunucu düzeyinde sunulur ve değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="69b97-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="69b97-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="69b97-106">Prerequisites</span></span>
<span data-ttu-id="69b97-107">toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="69b97-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="69b97-108">Sunucu ve veritabanına [PostgreSQL için bir Azure veritabanı oluşturma](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="69b97-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="69b97-109">Yükleme [Azure CLI 2.0](/cli/azure/install-azure-cli) komut satırı yardımcı programı veya kullanım hello Azure bulut Kabuk hello tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="69b97-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="69b97-110">Itanium tabanlı sistemler için liste sunucu yapılandırma parametreleri Azure veritabanı için PostgreSQL sunucusu</span><span class="sxs-lookup"><span data-stu-id="69b97-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="69b97-111">Tüm değiştirilebilir parametreler bir sunucu ve bunların değerleri toolist çalıştırmak hello [az postgres sunucu yapılandırması listesi](/cli/azure/postgres/server/configuration#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="69b97-111">toolist all modifiable parameters in a server and their values, run hello [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="69b97-112">Merhaba hello sunucusu için sunucu yapılandırma parametrelerini listeleyebilirsiniz **mypgserver 20170401.postgres.database.azure.com** kaynak grubu altında **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="69b97-112">You can list hello server configuration parameters for hello server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="69b97-113">Sunucu yapılandırması parametre ayrıntıları göster</span><span class="sxs-lookup"><span data-stu-id="69b97-113">Show server configuration parameter details</span></span>
<span data-ttu-id="69b97-114">Merhaba çalıştıran bir sunucu için belirli yapılandırma parametresi tooshow ayrıntılarını [az postgres sunucu yapılandırması Göster](/cli/azure/postgres/server/configuration#show) komutu.</span><span class="sxs-lookup"><span data-stu-id="69b97-114">tooshow details about a particular configuration parameter for a server, run hello [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="69b97-115">Bu örnek hello ayrıntılarını gösterir **günlük\_min\_iletileri** sunucusu için sunucu yapılandırma parametresi **mypgserver 20170401.postgres.database.azure.com** altında kaynak grubu **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="69b97-115">This example shows details of hello **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="69b97-116">Sunucu Yapılandırma parametresi değerini değiştirin</span><span class="sxs-lookup"><span data-stu-id="69b97-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="69b97-117">Belirli bir sunucu yapılandırma parametresi hello değerini de değiştirebilirsiniz ve bu hello PostgreSQL sunucu altyapısı için temel yapılandırma değeri hello güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="69b97-117">You can also modify hello value of a certain server configuration parameter, and this updates hello underlying configuration value for hello PostgreSQL server engine.</span></span> <span data-ttu-id="69b97-118">tooupdate hello yapılandırma kullanım hello [az postgres sunucu yapılandırma kümesi](/cli/azure/postgres/server/configuration#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="69b97-118">tooupdate hello configuration use hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="69b97-119">tooupdate hello **günlük\_min\_iletileri** sunucu yapılandırma parametresi sunucunun **mypgserver 20170401.postgres.database.azure.com** kaynakgrubundaki**myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="69b97-119">tooupdate hello **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="69b97-120">Tooreset hello yapılandırma parametresinin değerini istiyorsanız, isteğe bağlı hello çıkışı tooleave sadece tercih `--value` parametre ve hello hizmeti hello varsayılan değer uygulanacaktır.</span><span class="sxs-lookup"><span data-stu-id="69b97-120">If you want tooreset hello value of a configuration parameter, you simply choose tooleave out hello optional `--value` parameter, and hello service will apply hello default value.</span></span> <span data-ttu-id="69b97-121">İçinde Yukarıdaki örnek, onu gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="69b97-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="69b97-122">Bu hello sıfırlanacak **günlük\_min\_iletileri** yapılandırma toohello varsayılan değeri **uyarı**.</span><span class="sxs-lookup"><span data-stu-id="69b97-122">This will reset hello **log\_min\_messages** configuration toohello default value **WARNING**.</span></span> <span data-ttu-id="69b97-123">Sunucu Yapılandırması ve izin verilen değerlere daha ayrıntılı bilgi için üzerinde PostgreSQL belgelerine bakın. [sunucu yapılandırması](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span><span class="sxs-lookup"><span data-stu-id="69b97-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="69b97-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="69b97-124">Next steps</span></span>
- <span data-ttu-id="69b97-125">tooconfigure ve erişim sunucu günlüklerine bakın [PostgreSQL için Azure veritabanında sunucu günlükleri](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="69b97-125">tooconfigure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
