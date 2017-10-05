---
title: "SQL veritabanı için 1433 dışındaki bağlantı noktaları | Microsoft Docs"
description: "Azure SQL veritabanı ADO.NET'ten istemci bağlantılarını bazen proxy atlayabilir ve doğrudan veritabanıyla etkileşim. 1433 dışındaki bağlantı noktaları önemli hale gelmiştir."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: d47ee8c794d1e231507dae6bb4aa88bf19ce6418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="20b67-104">ADO.NET 4.5 için 1433 dışındaki bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="20b67-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="20b67-105">Bu konu, ADO.NET 4.5 veya sonraki bir sürümünü kullanan istemciler için Azure SQL veritabanı bağlantı davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="20b67-105">This topic describes the Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="20b67-106">Bağlantı mimarisi hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı bağlantısı mimarisi](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="20b67-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="20b67-107">Dış vs içinde</span><span class="sxs-lookup"><span data-stu-id="20b67-107">Outside vs inside</span></span>
<span data-ttu-id="20b67-108">Azure SQL veritabanı bağlantıları için biz ilk istemci programınız çalışıp çalışmayacağını başvurmalısınız *dışında* veya *içinde* Azure bulut sınır.</span><span class="sxs-lookup"><span data-stu-id="20b67-108">For connections to Azure SQL Database, we must first ask whether your client program runs *outside* or *inside* the Azure cloud boundary.</span></span> <span data-ttu-id="20b67-109">Alt bölümlerde iki yaygın senaryolar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="20b67-109">The subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="20b67-110">*Dış:* istemcisi, masaüstü bilgisayarınızda çalıştırır</span><span class="sxs-lookup"><span data-stu-id="20b67-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="20b67-111">Bağlantı noktası 1433 SQL veritabanı istemci uygulamanızı barındıran masaüstü bilgisayarınızda açık olması gerekir tek bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="20b67-111">Port 1433 is the only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="20b67-112">*İç:* istemci Azure üzerinde çalışır</span><span class="sxs-lookup"><span data-stu-id="20b67-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="20b67-113">İstemcinizin Azure bulut sınırının içinde çalıştığında, veririz kullandığı bir *doğrudan rota* SQL veritabanı sunucusu ile etkileşim.</span><span class="sxs-lookup"><span data-stu-id="20b67-113">When your client runs inside the Azure cloud boundary, it uses what we can call a *direct route* to interact with the SQL Database server.</span></span> <span data-ttu-id="20b67-114">Daha fazla bağlantı kurulduktan sonra istemci ve veritabanı arasındaki etkileşimler hiçbir ara proxy içerir.</span><span class="sxs-lookup"><span data-stu-id="20b67-114">After a connection is established, further interactions between the client and database involve no middleware proxy.</span></span>

<span data-ttu-id="20b67-115">Sıra aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="20b67-115">The sequence is as follows:</span></span>

1. <span data-ttu-id="20b67-116">ADO.NET 4.5 (veya üzeri) Azure bulut kısa bir etkileşim başlatır ve dinamik olarak tanımlanan bağlantı noktası numarasını alır.</span><span class="sxs-lookup"><span data-stu-id="20b67-116">ADO.NET 4.5 (or later) initiates a brief interaction with the Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="20b67-117">Dinamik olarak tanımlanan bağlantı noktası numarasını 11000 11999 veya 14000 14999 aralıktır.</span><span class="sxs-lookup"><span data-stu-id="20b67-117">The dynamically identified port number is in the range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="20b67-118">ADO.NET ardından SQL veritabanı sunucusuna doğrudan hiçbir Ara yazılımla arasında bağlanır.</span><span class="sxs-lookup"><span data-stu-id="20b67-118">ADO.NET then connects to the SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="20b67-119">Sorgular veritabanına doğrudan gönderilir ve sonuçları doğrudan istemciye döndürülür.</span><span class="sxs-lookup"><span data-stu-id="20b67-119">Queries are sent directly to the database, and results are returned directly to the client.</span></span>

<span data-ttu-id="20b67-120">11000 11999 ve Azure İstemci makinenizde 14000 14999 aralıklarına SQL veritabanı ile ADO.NET 4.5 istemci etkileşimler için kullanılabilir kalan bağlantı noktasının emin olun.</span><span class="sxs-lookup"><span data-stu-id="20b67-120">Ensure that the port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="20b67-121">Özellikle, aralığındaki bağlantı noktalarına diğer giden blockers boş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="20b67-121">In particular, ports in the range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="20b67-122">Azure VM'nizi üzerinde **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı** bağlantı noktası ayarlarını denetler.</span><span class="sxs-lookup"><span data-stu-id="20b67-122">On your Azure VM, the **Windows Firewall with Advanced Security** controls the port settings.</span></span>
  
  * <span data-ttu-id="20b67-123">Kullanabileceğiniz [güvenlik duvarının kullanıcı arabirimi](http://msdn.microsoft.com/library/cc646023.aspx) belirtmek için bir kural eklemek için **TCP** protokolü bir bağlantı noktası aralığı sözdizimi ile birlikte ister **11000 11999**.</span><span class="sxs-lookup"><span data-stu-id="20b67-123">You can use the [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) to add a rule for which you specify the **TCP** protocol along with a port range with the syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="20b67-124">Sürüm açıklamalar</span><span class="sxs-lookup"><span data-stu-id="20b67-124">Version clarifications</span></span>
<span data-ttu-id="20b67-125">Bu bölümde ürün sürümleri başvurmak adlar açıklar.</span><span class="sxs-lookup"><span data-stu-id="20b67-125">This section clarifies the monikers that refer to product versions.</span></span> <span data-ttu-id="20b67-126">Ayrıca, bazı ürünler arasındaki sürümleri eşleştirmelerini listeler.</span><span class="sxs-lookup"><span data-stu-id="20b67-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="20b67-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="20b67-127">ADO.NET</span></span>
* <span data-ttu-id="20b67-128">ADO.NET 4.0 TDS 7.3 protokolü, ancak değil 7.4 destekler.</span><span class="sxs-lookup"><span data-stu-id="20b67-128">ADO.NET 4.0 supports the TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="20b67-129">ADO.NET 4.5 ve sonraki TDS 7.4 protokolünü destekler.</span><span class="sxs-lookup"><span data-stu-id="20b67-129">ADO.NET 4.5 and later supports the TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="20b67-130">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="20b67-130">Related links</span></span>
* <span data-ttu-id="20b67-131">ADO.NET 4.6 20 Temmuz 2015 tarihinde yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="20b67-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="20b67-132">.NET ekibi Web günlüğü duyurudan kullanılabilir [burada](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="20b67-132">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="20b67-133">ADO.NET 4.5 15 Ağustos 2012'de serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="20b67-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="20b67-134">.NET ekibi Web günlüğü duyurudan kullanılabilir [burada](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="20b67-134">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="20b67-135">ADO.NET 4.5.1 hakkında bir blog gönderisini kullanılabilir [burada](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="20b67-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="20b67-136">TDS Protokolü sürüm listesi</span><span class="sxs-lookup"><span data-stu-id="20b67-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="20b67-137">SQL veritabanı geliştirme genel bakış</span><span class="sxs-lookup"><span data-stu-id="20b67-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="20b67-138">Azure SQL veritabanı güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="20b67-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="20b67-139">Nasıl yapılır: SQL veritabanında güvenlik duvarı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="20b67-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

