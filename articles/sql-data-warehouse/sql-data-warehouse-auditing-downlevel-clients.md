---
title: "aaaSQL veri ambarı alt düzey istemcileri destekleyen veri denetimi için | Microsoft Docs"
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
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="7430b-103">SQL Data Warehouse - denetime ve dinamik veri maskeleme için alt düzey istemci desteği</span><span class="sxs-lookup"><span data-stu-id="7430b-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="7430b-104">[Denetim](sql-data-warehouse-auditing-overview.md) TDS yeniden yönlendirmeyi destekleyen SQL istemcileri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="7430b-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="7430b-105">TDS 7.4 uygulayan herhangi bir istemci yeniden yönlendirme de desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="7430b-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="7430b-106">Özel durumlar toothis JDBC 4.0 yeniden yönlendirme değil uygulanmıştır Node.JS için hangi hello yeniden yönlendirme özelliğini tam olarak desteklenmiyor ve Tedious içerir.</span><span class="sxs-lookup"><span data-stu-id="7430b-106">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="7430b-107">"Alt düzey istemciler için", yani TDS sürüm 7.3 desteklemek ve aşağıda - server FQDN hello bağlantı dizesinde hello değiştirilmelidir:</span><span class="sxs-lookup"><span data-stu-id="7430b-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="7430b-108">Özgün sunucunun FQDN hello bağlantı dizesinde: <*sunucu adı*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="7430b-108">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="7430b-109">Merhaba bağlantı dizesinde değiştirilmiş sunucu FQDN: <*sunucu adı*> .database. **güvenli**. windows.net</span><span class="sxs-lookup"><span data-stu-id="7430b-109">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="7430b-110">"Alt düzey istemciler" kısmi bir listesine içerir:</span><span class="sxs-lookup"><span data-stu-id="7430b-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="7430b-111">.NET 4.0 ve aşağıdaki</span><span class="sxs-lookup"><span data-stu-id="7430b-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="7430b-112">ODBC 10.0 ve aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="7430b-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="7430b-113">(JDBC TDS 7.4, TDS yeniden yönlendirme özelliğini tam olarak desteklenmez hello desteklerken) JDBC</span><span class="sxs-lookup"><span data-stu-id="7430b-113">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="7430b-114">Can sıkıcı (için Node.JS)</span><span class="sxs-lookup"><span data-stu-id="7430b-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="7430b-115">**Açıklama:** hello sunucu FDQN değişikliği yukarıda bir yapılandırma gereksinimini adım olmadan her veritabanı (geçici azaltma) de bir SQL Server düzeyi denetim ilkesi uygulamak için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="7430b-115">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

