---
title: "Azure CLI kullanarak PostgreSQL için sunucu günlüklerine aaaConfigure ve erişim | Microsoft Docs"
description: "Bu makalede nasıl tooconfigure ve erişim hello Azure veritabanı'nda Azure CLI komut satırını kullanarak PostgreSQL için olay günlüklerini açıklanmaktadır."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="cb086-103">Yapılandırma ve Azure CLI kullanarak sunucu günlüklerine erişme</span><span class="sxs-lookup"><span data-stu-id="cb086-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="cb086-104">Merhaba PostgreSQL server Hata günlüklerini hello komut satırı arabirimi (Azure CLI) kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb086-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="cb086-105">Ancak, erişim tootransaction günlükleri desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cb086-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="cb086-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cb086-106">Prerequisites</span></span>
<span data-ttu-id="cb086-107">toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="cb086-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="cb086-108">Bir [PostgreSQL sunucu için Azure veritabanı](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="cb086-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="cb086-109">Yükleme [Azure CLI 2.0](/cli/azure/install-azure-cli) komut satırı yardımcı programı veya kullanım hello Azure bulut Kabuk hello tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="cb086-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="cb086-110">Azure veritabanı için günlük kaydını PostgreSQL için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cb086-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="cb086-111">Merhaba sunucu tooaccess sorgu günlüklerini ve Hata günlüklerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb086-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="cb086-112">Hata günlüklerini otomatik vakum, bağlantı ve kontrol noktaları bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="cb086-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="cb086-113">Günlüğünü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="cb086-113">Turn on logging</span></span>
2. <span data-ttu-id="cb086-114">Güncelleştirme günlük\_deyimi ve günlük\_min\_süresi\_deyimi tooenable sorgu günlüğü</span><span class="sxs-lookup"><span data-stu-id="cb086-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="cb086-115">Saklama dönemi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="cb086-115">Update retention period</span></span>

<span data-ttu-id="cb086-116">Daha fazla bilgi için bkz: [sunucu yapılandırma parametreleri özelleştirme](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cb086-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="cb086-117">Azure veritabanı için liste günlüklerini PostgreSQL sunucusu</span><span class="sxs-lookup"><span data-stu-id="cb086-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="cb086-118">Merhaba çalıştıran sunucunuz için toolist hello kullanılabilir günlük dosyalarını [az postgres sunucu günlükleri listesi](/cli/azure/postgres/server-logs#list) komutu.</span><span class="sxs-lookup"><span data-stu-id="cb086-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="cb086-119">Sunucu için hello günlük dosyalarını listeleyebilirsiniz **mypgserver 20170401.postgres.database.azure.com** kaynak grubu altında **myresourcegroup**ve tooa metni doğrudan adlı dosyaya **günlük\_dosyaları\_list.txt.**</span><span class="sxs-lookup"><span data-stu-id="cb086-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="cb086-120">Günlükleri hello sunucusundan yerel olarak yükle</span><span class="sxs-lookup"><span data-stu-id="cb086-120">Download logs locally from hello server</span></span>
<span data-ttu-id="cb086-121">Merhaba [az postgres server-günlükleri indirmek](/cli/azure/postgres/server-logs#download) komutu toodownload ayrı günlük dosyalarına sunucunuz için sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb086-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="cb086-122">İndirmeler hello hello sunucu için özel günlük dosyası Bu örnek **mypgserver 20170401.postgres.database.azure.com** kaynak grubu altında **myresourcegroup** tooyour yerel ortamı.</span><span class="sxs-lookup"><span data-stu-id="cb086-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="cb086-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cb086-123">Next steps</span></span>
- <span data-ttu-id="cb086-124">toolearn sunucu günlükleri hakkında daha fazla bilgi görmek [PostgreSQL için Azure veritabanında sunucu günlükleri](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="cb086-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="cb086-125">Sunucu parametreleri hakkında daha fazla bilgi için bkz: [Azure CLI kullanarak sunucu yapılandırma parametreleri özelleştirme](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="cb086-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
