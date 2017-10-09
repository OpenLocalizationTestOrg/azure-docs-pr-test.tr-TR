---
title: "SQL veritabanı için aaaConnection kitaplıkları | Microsoft Docs"
description: "Bağlantı tooSQL sunucusu ve çok çeşitli programlama dillerinde istemci SQL veritabanı etkinleştiren modüllerin yüklemeler için bağlantılar sağlar. Merhaba modülleri hello topluluk veya Microsoft tarafından kullanıma sunulur."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: genemi
ms.assetid: 13d899d3-cf46-4e4d-8919-cf4b41ca836d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: genemi
ms.openlocfilehash: 6ea77670276ad3304c7531f7ffd8f7dffd31af46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Bağlantı kitaplıklarını ve çerçevelerini Microsoft SQL Server için

Kullanıma bizim [Başlarken öğreticilerine alma](http://aka.ms/sqldev) tooquickly dil C#, Java, Node.js, PHP ve Python gibi programlama ile başlayın ve SQL Server üzerinde macOS Linux veya Windows veya Docker kullanarak bir uygulama oluşturun.

Merhaba aşağıdaki tabloda bağlantı kitaplıkları veya *sürücüleri* istemci uygulamaları dilleri tooconnect tooand kullanım şirket içi çalışan Microsoft SQL Server veya Linux, Windows veya Docker hello bulutta değişik kullanabilir ve Ayrıca tooAzure SQL Database ve Azure SQL veri ambarı. 

| Dil | Platform | Ek kaynaklar | İndir | Kullanmaya Başlama |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [SQL Server için Microsoft ADO.NET](https://docs.microsoft.com/sql/connect/ado-net/microsoft-ado-net-for-sql-server) | [İndir](https://www.microsoft.com/net/download/) | [Kullanmaya Başlama](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [SQL Server için Microsoft JDBC sürücüsü](http://msdn.microsoft.com/library/mt484311.aspx) | [İndir](https://go.microsoft.com/fwlink/?linkid=852460) |  [Kullanmaya Başlama](https://www.microsoft.com/en-us/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [SQL Server için PHP SQL sürücüsü](http://msdn.microsoft.com/library/dn865013.aspx) | İşletim Sistemi: <br/> \*[Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \*[Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \*[macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [Kullanmaya Başlama](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [SQL Server için node.js sürücüsü](http://msdn.microsoft.com/library/mt652093.aspx) | [Yükleme](https://msdn.microsoft.com/library/mt652094.aspx) |  [Kullanmaya Başlama](https://www.microsoft.com/en-us/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Python SQL sürücüsü](http://msdn.microsoft.com/library/mt652092.aspx) | Seçimler yükleyin: <br/> \*[pymssql](https://msdn.microsoft.com/library/mt694094.aspx) <br/> \*[pyodbc](http://msdn.microsoft.com/library/mt763257.aspx) |  [Kullanmaya Başlama](https://www.microsoft.com/en-us/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [SQL Server için Söyleniş sürücüsü](http://msdn.microsoft.com/library/mt691981.aspx) | [Yükleme](https://msdn.microsoft.com/library/mt711041.aspx) | [Kullanmaya Başlama](https://www.microsoft.com/en-us/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [SQL Server için Microsoft ODBC sürücüsü](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) | [İndir](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) |  

Merhaba aşağıdaki tabloda listelenmektedir nesne ilişkisel eşleme (ORM) çerçeveler ve istemci uygulamaları veya şirket içi çalışan Microsoft SQL Server ile kullanabileceğiniz web çerçeveleri Linux, Windows veya Docker ve ayrıca tooAzure SQL veritabanı hello bulutta birkaç örnekleri ve Azure SQL veri ambarı. 

| Dil | Platform | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/en-us/ef)<br>[Entity Framework Çekirdek](https://docs.microsoft.com/en-us/ef/core/index) |
| Java | Windows, Linux, macOS |[ORM hazırda bekleme](http://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [ORM sequelize](http://docs.sequelizejs.com) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby rayları üzerinde](http://rubyonrails.org/) |

## <a name="related-links"></a>İlgili bağlantılar
- [SQL Server sürücüleri](http://msdn.microsoft.com/library/mt654049.aspx) istemci uygulamalarından bağlamak için
- [.NET (C#) kullanarak tooSQL veritabanına bağlanma](sql-database-connect-query-dotnet.md)
- [PHP kullanarak tooSQL veritabanına bağlanma](sql-database-connect-query-php.md)
- [Node.js kullanarak tooSQL veritabanına bağlanma](sql-database-connect-query-nodejs.md)
- [Java kullanarak tooSQL veritabanına bağlanma](sql-database-connect-query-java.md)
- [Python kullanarak tooSQL veritabanına bağlanma](sql-database-connect-query-python.md)
- [Ruby kullanarak tooSQL veritabanına bağlanma](sql-database-connect-query-ruby.md)
