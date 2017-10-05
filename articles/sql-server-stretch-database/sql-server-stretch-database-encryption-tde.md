---
title: "Saydam veri şifreleme Esnetme veritabanı - Azure için etkinleştirme | Microsoft Docs"
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
ms.openlocfilehash: ceb355d2ba872ed5d3886c6dc82ca75b1854db0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="edbdb-103">Azure üzerinde Esnetme veritabanı için saydam veri şifreleme (TDE) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="edbdb-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="edbdb-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="edbdb-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="edbdb-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="edbdb-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="edbdb-106">Saydam veri şifreleme (TDE) gerçek zamanlı şifreleme ve şifre çözme veritabanının, ilişkili yedeklemelerinizi ve geri kalan işlem günlüğü dosyalarını uygulamasında yapılacak değişiklikler gerek kalmadan gerçekleştirerek kötü amaçlı etkinliği tehdide karşı korunmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="edbdb-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="edbdb-107">TDE, veritabanının tamamını Depolama veritabanı şifreleme anahtarını adlı bir simetrik anahtar kullanarak şifreler.</span><span class="sxs-lookup"><span data-stu-id="edbdb-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="edbdb-108">Veritabanı şifreleme anahtarını bir yerleşik bir sunucu sertifikası tarafından korunur.</span><span class="sxs-lookup"><span data-stu-id="edbdb-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="edbdb-109">Yerleşik bir sunucu sertifikası Azure her sunucu için benzersizdir.</span><span class="sxs-lookup"><span data-stu-id="edbdb-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="edbdb-110">Microsoft, bu sertifikalar otomatik olarak en az 90 günde döndürür.</span><span class="sxs-lookup"><span data-stu-id="edbdb-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="edbdb-111">TDE genel bir açıklaması için bkz [saydam veri şifreleme (TDE)].</span><span class="sxs-lookup"><span data-stu-id="edbdb-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="edbdb-112">Şifrelemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="edbdb-112">Enabling Encryption</span></span>
<span data-ttu-id="edbdb-113">TDE Azure etkinleştirmek için bir SQL Server Esnetme etkinleştirilmiş veritabanından veri depolama veritabanı geçişi, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="edbdb-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="edbdb-114">Veritabanında açmak [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="edbdb-114">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="edbdb-115">Veritabanı dikey penceresinde tıklayın **ayarları** düğmesi</span><span class="sxs-lookup"><span data-stu-id="edbdb-115">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="edbdb-116">Seçin **saydam veri şifreleme** seçeneği![][1]</span><span class="sxs-lookup"><span data-stu-id="edbdb-116">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="edbdb-117">Seçin **üzerinde** ayarlama ve ardından **Kaydet**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="edbdb-117">Select the **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="edbdb-118">Şifreleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="edbdb-118">Disabling Encryption</span></span>
<span data-ttu-id="edbdb-119">Azure TDE devre dışı bırakmak için bir SQL Server Esnetme etkinleştirilmiş veritabanından veri depolama veritabanı geçişi, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="edbdb-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="edbdb-120">Veritabanında açmak [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="edbdb-120">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="edbdb-121">Veritabanı dikey penceresinde tıklayın **ayarları** düğmesi</span><span class="sxs-lookup"><span data-stu-id="edbdb-121">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="edbdb-122">Seçin **saydam veri şifreleme** seçeneği</span><span class="sxs-lookup"><span data-stu-id="edbdb-122">Select the **Transparent data encryption** option</span></span>
4. <span data-ttu-id="edbdb-123">Seçin **kapalı** ayarlama ve ardından **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="edbdb-123">Select the **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
<span data-ttu-id="edbdb-124">[saydam veri şifreleme (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="edbdb-124">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
