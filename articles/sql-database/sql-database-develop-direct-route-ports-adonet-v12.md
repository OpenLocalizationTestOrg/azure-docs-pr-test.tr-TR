---
title: "SQL veritabanı için 1433 ötesinde aaaPorts | Microsoft Docs"
description: "ADO.NET tooAzure SQL veritabanı'ten istemci bağlantılarını bazen hello proxy atlayabilir ve doğrudan hello veritabanıyla etkileşim. 1433 dışındaki bağlantı noktaları önemli hale gelmiştir."
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
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="d64f3-104">ADO.NET 4.5 için 1433 dışındaki bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="d64f3-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="d64f3-105">Bu konu, ADO.NET 4.5 veya sonraki bir sürümünü kullanan istemciler için hello Azure SQL veritabanı bağlantı davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d64f3-105">This topic describes hello Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d64f3-106">Bağlantı mimarisi hakkında daha fazla bilgi için bkz: [Azure SQL veritabanı bağlantısı mimarisi](sql-database-connectivity-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="d64f3-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="d64f3-107">Dış vs içinde</span><span class="sxs-lookup"><span data-stu-id="d64f3-107">Outside vs inside</span></span>
<span data-ttu-id="d64f3-108">Bağlantıları tooAzure SQL veritabanı için biz ilk istemci programınız çalışıp çalışmayacağını başvurmalısınız *dışında* veya *içinde* hello Azure bulut sınır.</span><span class="sxs-lookup"><span data-stu-id="d64f3-108">For connections tooAzure SQL Database, we must first ask whether your client program runs *outside* or *inside* hello Azure cloud boundary.</span></span> <span data-ttu-id="d64f3-109">Merhaba alt bölümlerde iki yaygın senaryolar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d64f3-109">hello subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="d64f3-110">*Dış:* istemcisi, masaüstü bilgisayarınızda çalıştırır</span><span class="sxs-lookup"><span data-stu-id="d64f3-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="d64f3-111">Bağlantı noktası 1433 SQL veritabanı istemci uygulamanızı barındıran masaüstü bilgisayarınızda açılmalıdır hello tek bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="d64f3-111">Port 1433 is hello only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="d64f3-112">*İç:* istemci Azure üzerinde çalışır</span><span class="sxs-lookup"><span data-stu-id="d64f3-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="d64f3-113">İstemciniz hello Azure bulut sınırının içinde çalıştığında, veririz kullandığı bir *doğrudan rota* toointeract hello SQL veritabanı sunucusu ile.</span><span class="sxs-lookup"><span data-stu-id="d64f3-113">When your client runs inside hello Azure cloud boundary, it uses what we can call a *direct route* toointeract with hello SQL Database server.</span></span> <span data-ttu-id="d64f3-114">Bağlantı kurulduktan sonra daha sonraki etkileşimler hello istemci ve veritabanı arasındaki hiçbir ara proxy içerir.</span><span class="sxs-lookup"><span data-stu-id="d64f3-114">After a connection is established, further interactions between hello client and database involve no middleware proxy.</span></span>

<span data-ttu-id="d64f3-115">Merhaba dizisi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d64f3-115">hello sequence is as follows:</span></span>

1. <span data-ttu-id="d64f3-116">ADO.NET 4.5 (veya üzeri) hello Azure bulut kısa bir etkileşim başlatır ve dinamik olarak tanımlanan bağlantı noktası numarasını alır.</span><span class="sxs-lookup"><span data-stu-id="d64f3-116">ADO.NET 4.5 (or later) initiates a brief interaction with hello Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="d64f3-117">11000 11999 veya 14000 14999 hello aralıkta dinamik olarak tanımlanan hello bağlantı noktası numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="d64f3-117">hello dynamically identified port number is in hello range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="d64f3-118">ADO.NET ardından toohello SQL veritabanı sunucusuna doğrudan hiçbir Ara yazılımla arasında bağlanır.</span><span class="sxs-lookup"><span data-stu-id="d64f3-118">ADO.NET then connects toohello SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="d64f3-119">Sorgular doğrudan toohello veritabanı gönderilir ve sonuçları doğrudan toohello istemci döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d64f3-119">Queries are sent directly toohello database, and results are returned directly toohello client.</span></span>

<span data-ttu-id="d64f3-120">11000 11999 ve Azure İstemci makinenizde 14000 14999 aralıklarına SQL veritabanı ile ADO.NET 4.5 istemci etkileşimler için kullanılabilir kalan o hello bağlantı noktası emin olun.</span><span class="sxs-lookup"><span data-stu-id="d64f3-120">Ensure that hello port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="d64f3-121">Özellikle, hello aralığındaki bağlantı noktalarına diğer giden blockers boş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d64f3-121">In particular, ports in hello range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="d64f3-122">Azure VM'nizi hello **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı** denetimleri hello bağlantı noktası ayarları.</span><span class="sxs-lookup"><span data-stu-id="d64f3-122">On your Azure VM, hello **Windows Firewall with Advanced Security** controls hello port settings.</span></span>
  
  * <span data-ttu-id="d64f3-123">Merhaba kullanabilirsiniz [güvenlik duvarının kullanıcı arabirimi](http://msdn.microsoft.com/library/cc646023.aspx) hello belirttiğiniz kuralı bir tooadd **TCP** protokolü bir bağlantı noktası aralığı hello sözdizimi ile birlikte ister **11000 11999**.</span><span class="sxs-lookup"><span data-stu-id="d64f3-123">You can use hello [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a rule for which you specify hello **TCP** protocol along with a port range with hello syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="d64f3-124">Sürüm açıklamalar</span><span class="sxs-lookup"><span data-stu-id="d64f3-124">Version clarifications</span></span>
<span data-ttu-id="d64f3-125">Bu bölümde tooproduct sürümleri başvuran hello adlar açıklar.</span><span class="sxs-lookup"><span data-stu-id="d64f3-125">This section clarifies hello monikers that refer tooproduct versions.</span></span> <span data-ttu-id="d64f3-126">Ayrıca, bazı ürünler arasındaki sürümleri eşleştirmelerini listeler.</span><span class="sxs-lookup"><span data-stu-id="d64f3-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="d64f3-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="d64f3-127">ADO.NET</span></span>
* <span data-ttu-id="d64f3-128">ADO.NET 4.0 hello TDS 7.3 protokolünü kullanır, ancak değil 7.4 destekler.</span><span class="sxs-lookup"><span data-stu-id="d64f3-128">ADO.NET 4.0 supports hello TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="d64f3-129">ADO.NET 4.5 ve sonraki hello TDS 7.4 protokolünü destekler.</span><span class="sxs-lookup"><span data-stu-id="d64f3-129">ADO.NET 4.5 and later supports hello TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="d64f3-130">İlgili bağlantılar</span><span class="sxs-lookup"><span data-stu-id="d64f3-130">Related links</span></span>
* <span data-ttu-id="d64f3-131">ADO.NET 4.6 20 Temmuz 2015 tarihinde yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d64f3-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="d64f3-132">Merhaba .NET ekibi Web günlüğü duyurudan kullanılabilir [burada](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="d64f3-132">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="d64f3-133">ADO.NET 4.5 15 Ağustos 2012'de serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="d64f3-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="d64f3-134">Merhaba .NET ekibi Web günlüğü duyurudan kullanılabilir [burada](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="d64f3-134">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="d64f3-135">ADO.NET 4.5.1 hakkında bir blog gönderisini kullanılabilir [burada](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="d64f3-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="d64f3-136">TDS Protokolü sürüm listesi</span><span class="sxs-lookup"><span data-stu-id="d64f3-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="d64f3-137">SQL veritabanı geliştirme genel bakış</span><span class="sxs-lookup"><span data-stu-id="d64f3-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="d64f3-138">Azure SQL veritabanı güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="d64f3-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="d64f3-139">Nasıl yapılır: SQL veritabanında güvenlik duvarı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d64f3-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

