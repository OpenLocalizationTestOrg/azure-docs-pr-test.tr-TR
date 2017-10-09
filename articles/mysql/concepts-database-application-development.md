---
title: "Azure veritabanı için MySQL aaaDatabase uygulaması geliştirmeye genel bakış | Microsoft Docs"
description: "Bir geliştirici uygulama kodu tooconnect tooAzure veritabanı için MySQL yazılırken izlemeniz gereken tasarım konuları sunar"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="9592b-103">Azure veritabanı için MySQL için uygulama geliştirmeye genel bakış</span><span class="sxs-lookup"><span data-stu-id="9592b-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="9592b-104">Bu makalede, bir geliştirici uygulama kodu tooconnect tooAzure veritabanı için MySQL yazılırken izlemeniz gereken tasarım konuları anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9592b-104">This article discusses design considerations that a developer should follow when writing application code tooconnect tooAzure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="9592b-105">Toocreate bir sunucu oluşturmak nasıl sunucu tabanlı güvenlik duvarı, sunucu özellikleri görüntülemek, veritabanı oluşturma, bağlanma ve sorgulama çalışma ekranı ve mysql.exe kullanarak bir öğretici gösteren için bkz: [ilk Azure MySQL veritabanınızı tasarlama](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9592b-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="9592b-106">Dil ve platform</span><span class="sxs-lookup"><span data-stu-id="9592b-106">Language and platform</span></span>
<span data-ttu-id="9592b-107">Çeşitli programlama dilleri ve platformları için kod örnekleri mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="9592b-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="9592b-108">Toohello kod örnekleri, bağlantılar bulabilirsiniz: [bağlantı kitaplıkları kullanılan tooconnect tooAzure veritabanı için MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="9592b-108">You can find links toohello code samples at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="9592b-109">Araçlar</span><span class="sxs-lookup"><span data-stu-id="9592b-109">Tools</span></span>
<span data-ttu-id="9592b-110">Azure veritabanı için MySQL kullanır hello MySQL community sürümü, MySQL genel yönetim araçlarını mysql.exe gibi çalışma ekranı veya MySQL yardımcı programları gibi uyumlu [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)ve diğerleri.</span><span class="sxs-lookup"><span data-stu-id="9592b-110">Azure Database for MySQL uses hello MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="9592b-111">Merhaba veritabanı hizmeti ile Merhaba Azure portal, Azure CLI ve REST API'leri toointeract de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9592b-111">You can also use hello Azure portal, Azure CLI, and REST APIs toointeract with hello database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="9592b-112">Kaynak sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="9592b-112">Resource limitations</span></span>
<span data-ttu-id="9592b-113">Azure MySQL veritabanı iki farklı mekanizmalarını kullanarak hello kaynakları kullanılabilir tooa sunucusu yönetir:</span><span class="sxs-lookup"><span data-stu-id="9592b-113">Azure MySQL Database manages hello resources available tooa server using two different mechanisms:</span></span> 
- <span data-ttu-id="9592b-114">Kaynak Yönetimi</span><span class="sxs-lookup"><span data-stu-id="9592b-114">Resources Governance</span></span> 
- <span data-ttu-id="9592b-115">Sınırları zorlama.</span><span class="sxs-lookup"><span data-stu-id="9592b-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="9592b-116">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="9592b-116">Security</span></span>
<span data-ttu-id="9592b-117">Azure MySQL veritabanı sınırlama erişim, koruma verileri, yapılandırma kullanıcılar ve rolü ve bir MySQL veritabanı etkinliklerini izleme için kaynaklar sağlar.</span><span class="sxs-lookup"><span data-stu-id="9592b-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="9592b-118">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="9592b-118">Authentication</span></span>
<span data-ttu-id="9592b-119">Azure MySQL veritabanı sunucu kimlik doğrulaması kullanıcı ve oturum açma bilgileri destekler.</span><span class="sxs-lookup"><span data-stu-id="9592b-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="9592b-120">Dayanıklılık</span><span class="sxs-lookup"><span data-stu-id="9592b-120">Resiliency</span></span>
<span data-ttu-id="9592b-121">TooMySQL veritabanına bağlanırken geçici bir hata ortaya çıktığında, kodunuzu hello çağrı yeniden denemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9592b-121">When a transient error occurs while connecting tooMySQL Database, your code should retry hello call.</span></span> <span data-ttu-id="9592b-122">Böylece, hello SQL veritabanı ile birden çok istemci aynı anda yeniden deneniyor doldurmaya değil hello yeniden deneme mantığı kullanım geri alma mantığı, öneririz.</span><span class="sxs-lookup"><span data-stu-id="9592b-122">We recommend hello retry logic use back off logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="9592b-123">Kod örnekleri: hello dili için örnek gösteren kod örnekleri mantığı yeniden denemek için bkz: [bağlantı kitaplıkları kullanılan tooconnect tooAzure veritabanı için MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="9592b-123">Code samples: For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="9592b-124">Bağlantıları Yönetme</span><span class="sxs-lookup"><span data-stu-id="9592b-124">Managing Connections</span></span>
<span data-ttu-id="9592b-125">Veritabanı bağlantıları sınırlı bir kaynak olduğundan, bağlantı duyarlı kullanmayı, MySQL veritabanınızı erişirken tooachieve daha iyi performans öneririz.</span><span class="sxs-lookup"><span data-stu-id="9592b-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database tooachieve better performance.</span></span>
- <span data-ttu-id="9592b-126">Bağlantı havuzu veya kalıcı bağlantılar kullanarak hello veritabanı erişim.</span><span class="sxs-lookup"><span data-stu-id="9592b-126">Access hello database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="9592b-127">Kısa bağlantı ömrü kullanarak hello veritabanı erişim.</span><span class="sxs-lookup"><span data-stu-id="9592b-127">Access hello database by using short connection life span.</span></span> 
- <span data-ttu-id="9592b-128">Kullanım yeniden deneme mantığı uygulamanızda hello bağlantı girişimi, toocatch hataları tooconcurrent bağlantılar nedeniyle hello noktada hello maksimum izin verilen ulaştı.</span><span class="sxs-lookup"><span data-stu-id="9592b-128">Use retry logic in your application at hello point of hello connection attempt, toocatch failures due tooconcurrent connections have reached hello maximum allowed.</span></span> <span data-ttu-id="9592b-129">Merhaba mantığı yeniden deneyin ve kısa bir gecikme ayarlama hello ek bağlantı denemeleri önce rastgele bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="9592b-129">In hello retry logic, set a short delay, and then wait for a random time before hello additional connection attempts.</span></span>
