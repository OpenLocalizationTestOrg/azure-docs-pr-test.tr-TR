---
title: "Saydam veri şifreleme için Esnetme veritabanı - Azure aaaEnable | Microsoft Docs"
description: "Saydam veri şifreleme (TDE) Azure üzerinde SQL Server Esnetme veritabanı için etkinleştirin"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="911f8-103">Azure üzerinde Esnetme veritabanı için saydam veri şifreleme (TDE) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="911f8-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="911f8-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="911f8-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="911f8-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="911f8-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="911f8-106">Saydam veri şifreleme (TDE) gerçek zamanlı şifreleme ve şifre çözme hello veritabanının, ilişkili yedeklemelerinizi ve geri kalan işlem günlüğü dosyalarını değişiklikleri toohello gerek kalmadan gerçekleştirerek kötü amaçlı etkinliği hello tehdide karşı korunmasına yardımcı olur. uygulama.</span><span class="sxs-lookup"><span data-stu-id="911f8-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="911f8-107">TDE, bir simetrik anahtar adlı hello veritabanı şifreleme anahtarı kullanarak veritabanının tamamını hello depolanmasını şifreler.</span><span class="sxs-lookup"><span data-stu-id="911f8-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="911f8-108">Merhaba veritabanı şifreleme anahtarı, bir yerleşik bir sunucu sertifikası tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="911f8-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="911f8-109">Merhaba yerleşik bir sunucu sertifikası Azure her sunucu için benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="911f8-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="911f8-110">Microsoft, bu sertifikalar otomatik olarak en az 90 günde döndürür.</span><span class="sxs-lookup"><span data-stu-id="911f8-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="911f8-111">TDE genel bir açıklaması için bkz [saydam veri şifreleme (TDE)].</span><span class="sxs-lookup"><span data-stu-id="911f8-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="911f8-112">Şifrelemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="911f8-112">Enabling Encryption</span></span>
<span data-ttu-id="911f8-113">bir SQL Server Esnetme etkinleştirilmiş veritabanından veri geçişi hello depolama Azure bir veritabanı için tooenable TDE hello şeyler aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="911f8-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="911f8-114">Merhaba açık hello veritabanında [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="911f8-114">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="911f8-115">Merhaba veritabanı dikey penceresinde hello tıklayın **ayarları** düğmesi</span><span class="sxs-lookup"><span data-stu-id="911f8-115">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="911f8-116">Select hello **saydam veri şifreleme** seçeneği![][1]</span><span class="sxs-lookup"><span data-stu-id="911f8-116">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="911f8-117">Select hello **üzerinde** ayarlama ve ardından **Kaydet**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="911f8-117">Select hello **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="911f8-118">Şifreleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="911f8-118">Disabling Encryption</span></span>
<span data-ttu-id="911f8-119">bir SQL Server Esnetme etkinleştirilmiş veritabanından veri geçişi hello depolama Azure bir veritabanı için toodisable TDE hello şeyler aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="911f8-119">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="911f8-120">Merhaba açık hello veritabanında [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="911f8-120">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="911f8-121">Merhaba veritabanı dikey penceresinde hello tıklayın **ayarları** düğmesi</span><span class="sxs-lookup"><span data-stu-id="911f8-121">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="911f8-122">Select hello **saydam veri şifreleme** seçeneği</span><span class="sxs-lookup"><span data-stu-id="911f8-122">Select hello **Transparent data encryption** option</span></span>
4. <span data-ttu-id="911f8-123">Select hello **kapalı** ayarlama ve ardından **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="911f8-123">Select hello **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[saydam veri şifreleme (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
