---
title: "SQL veri ambarı alt düzey istemcileri destekleyen veri denetimi için | Microsoft Docs"
description: "Verileri denetlemek için SQL Data Warehouse alt düzey istemci desteği hakkında bilgi edinin"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: a7ea6141285a0098339f1e071af2592dd4535c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="9ed50-103">SQL Data Warehouse - denetime ve dinamik veri maskeleme için alt düzey istemci desteği</span><span class="sxs-lookup"><span data-stu-id="9ed50-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="9ed50-104">[Denetim](sql-data-warehouse-auditing-overview.md) TDS yeniden yönlendirmeyi destekleyen SQL istemcileri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="9ed50-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="9ed50-105">TDS 7.4 uygulayan herhangi bir istemci yeniden yönlendirme de desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="9ed50-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="9ed50-106">Bu özel durumlar yeniden yönlendirme özelliğini tam olarak desteklenmez ve Node.JS hangi yeniden yönlendirmesi için Tedious uygulanmadı JDBC 4.0 içerir.</span><span class="sxs-lookup"><span data-stu-id="9ed50-106">Exceptions to this include JDBC 4.0 in which the redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="9ed50-107">"Alt düzey istemciler için", yani hangi destek TDS sürüm 7.3 ve aşağıda - sunucunun FQDN bağlantı dizesi değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="9ed50-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - the server FQDN in the connection string should be modified:</span></span>

<span data-ttu-id="9ed50-108">Bağlantı dizesindeki özgün sunucunun FQDN: <*sunucu adı*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="9ed50-108">Original server FQDN in the connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="9ed50-109">Bağlantı dizesindeki değiştirilmiş sunucu FQDN: <*sunucu adı*> .database. **güvenli**. windows.net</span><span class="sxs-lookup"><span data-stu-id="9ed50-109">Modified server FQDN in the connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="9ed50-110">"Alt düzey istemciler" kısmi bir listesine içerir:</span><span class="sxs-lookup"><span data-stu-id="9ed50-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="9ed50-111">.NET 4.0 ve aşağıdaki</span><span class="sxs-lookup"><span data-stu-id="9ed50-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="9ed50-112">ODBC 10.0 ve aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="9ed50-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="9ed50-113">JDBC (JDBC TDS 7.4 desteklerken, bu TDS yeniden yönlendirme özelliğini tam olarak desteklenmez)</span><span class="sxs-lookup"><span data-stu-id="9ed50-113">JDBC (while JDBC does support TDS 7.4, the TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="9ed50-114">Can sıkıcı (için Node.JS)</span><span class="sxs-lookup"><span data-stu-id="9ed50-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="9ed50-115">**Açıklama:** yukarıdaki sunucunun FDQN değişikliği bir yapılandırma gereksinimini adım olmadan her veritabanı (geçici azaltma) de bir SQL Server düzeyi denetim ilkesi uygulamak için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="9ed50-115">**Remark:** The above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

