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
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a>SQL Data Warehouse - denetime ve dinamik veri maskeleme için alt düzey istemci desteği
[Denetim](sql-data-warehouse-auditing-overview.md) TDS yeniden yönlendirmeyi destekleyen SQL istemcileri ile çalışır.

TDS 7.4 uygulayan herhangi bir istemci yeniden yönlendirme de desteklemelidir. Özel durumlar toothis JDBC 4.0 yeniden yönlendirme değil uygulanmıştır Node.JS için hangi hello yeniden yönlendirme özelliğini tam olarak desteklenmiyor ve Tedious içerir.

"Alt düzey istemciler için", yani TDS sürüm 7.3 desteklemek ve aşağıda - server FQDN hello bağlantı dizesinde hello değiştirilmelidir:

Özgün sunucunun FQDN hello bağlantı dizesinde: <*sunucu adı*>. database.windows.net

Merhaba bağlantı dizesinde değiştirilmiş sunucu FQDN: <*sunucu adı*> .database. **güvenli**. windows.net

"Alt düzey istemciler" kısmi bir listesine içerir:

* .NET 4.0 ve aşağıdaki
* ODBC 10.0 ve aşağıdaki.
* (JDBC TDS 7.4, TDS yeniden yönlendirme özelliğini tam olarak desteklenmez hello desteklerken) JDBC
* Can sıkıcı (için Node.JS)

**Açıklama:** hello sunucu FDQN değişikliği yukarıda bir yapılandırma gereksinimini adım olmadan her veritabanı (geçici azaltma) de bir SQL Server düzeyi denetim ilkesi uygulamak için yararlı olabilir.     

