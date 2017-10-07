---
title: aaaConnect tooAzure SQL Data Warehouse | Microsoft Docs
description: "Nasıl tooAzure SQL Data Warehouse toofind hello sunucu adını ve bağlantı dizesi"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: e52872ca-ae74-4e25-9c56-d49c85c8d0f0
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: f15e098026afb7c5efbbbfaf62b681e8cd7936bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-sql-data-warehouse"></a>SQL veri ambarı tooAzure Bağlan
Bu makalede hello için ilk kez bağlı tooSQL veri ambarı size yardımcı olur.

## <a name="find-your-server-name"></a>Sunucu adınızı bulma
İlk adım tooconnecting tooSQL olan veri ambarı bilmek hello nasıl toofind sunucunuzun adı.  Örneğin, aşağıdaki örneğine hello hello sunucu adı sample.database.windows.net olur. toofind hello tam sunucu adı:

1. Toohello Git [Azure portal][Azure portal].
2. **SQL veritabanları**’na tıklayın 
3. Tooconnect için istediğiniz hello veritabanı tıklayın.
4. Merhaba tam sunucu adını bulun.
   
    ![Tam sunucu adı][1]

## <a name="supported-drivers-and-connection-strings"></a>Desteklenen sürücüler ve bağlantı dizeleri
Azure SQL Veri Ambarı; [ADO.NET][ADO.NET], [ODBC][ODBC], [PHP][PHP] ve [JDBC][JDBC]’yi destekler. Merhaba birini tıklatın sürücüleri toofind hello en son sürümünü ve belgeleri önceki. tooautomatically oluşturmak için kullanmakta olduğunuz hello sürücü hello bağlantı dizesi hello Azure ' üzerinde hello tıklatabilirsiniz portal, **veritabanı bağlantı dizelerini Göster** örnek önceki hello gelen.  Aşağıda ayrıca her sürücü için bir bağlantı dizesinin nasıl göründüğü ile ilgili bazı örnekler verilmiştir.

> [!NOTE]
> Bağlantı toosurvive kısa kullanılamazlık dönemlerini hello bağlantı zaman aşımı too300 saniye tooallow ayarlamayı göz önünde bulundurun.
> 
> 

### <a name="adonet-connection-string-example"></a>ADO.NET bağlantı dizesi örneği
```C#
Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};User ID={your_user_name};Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

### <a name="odbc-connection-string-example"></a>ODBC bağlantı dizesi örneği
```C#
Driver={SQL Server Native Client 11.0};Server=tcp:{your_server}.database.windows.net,1433;Database={your_database};Uid={your_user_name};Pwd={your_password_here};Encrypt=yes;TrustServerCertificate=no;Connection Timeout=30;
```

### <a name="php-connection-string-example"></a>PHP bağlantı dizesi örneği
```PHP
Server: {your_server}.database.windows.net,1433 \r\nSQL Database: {your_database}\r\nUser Name: {your_user_name}\r\n\r\nPHP Data Objects(PDO) Sample Code:\r\n\r\ntry {\r\n   $conn = new PDO ( \"sqlsrv:server = tcp:{your_server}.database.windows.net,1433; Database = {your_database}\", \"{your_user_name}\", \"{your_password_here}\");\r\n    $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );\r\n}\r\ncatch ( PDOException $e ) {\r\n   print( \"Error connecting tooSQL Server.\" );\r\n   die(print_r($e));\r\n}\r\n\rSQL Server Extension Sample Code:\r\n\r\n$connectionInfo = array(\"UID\" => \"{your_user_name}\", \"pwd\" => \"{your_password_here}\", \"Database\" => \"{your_database}\", \"LoginTimeout\" => 30, \"Encrypt\" => 1, \"TrustServerCertificate\" => 0);\r\n$serverName = \"tcp:{your_server}.database.windows.net,1433\";\r\n$conn = sqlsrv_connect($serverName, $connectionInfo);
```

### <a name="jdbc-connection-string-example"></a>JDBC bağlantı dizesi örneği
```Java
jdbc:sqlserver://yourserver.database.windows.net:1433;database=yourdatabase;user={your_user_name};password={your_password_here};encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
```

## <a name="connection-settings"></a>Bağlantı ayarları
SQL Veri Ambarı, bağlantı ve nesne oluşturma sırasında bazı ayarları standart hale getirir. Bu ayarlar geçersiz kılınamaz ve şunları içerir:

| Veritabanı Ayarı | Değer |
|:--- |:--- |
| [ANSI_NULLS][ANSI_NULLS] |AÇIK |
| [QUOTED_IDENTIFIERS][QUOTED_IDENTIFIERS] |AÇIK |
| [DATEFORMAT][DATEFORMAT] |mdy |
| [DATEFIRST][DATEFIRST] |7 |

## <a name="next-steps"></a>Sonraki adımlar
bkz: tooconnect ve Visual Studio ile sorgu [sorgu Visual Studio ile][Query with Visual Studio]. kimlik doğrulama seçenekleri hakkında daha fazla toolearn bkz [kimlik doğrulaması tooAzure SQL Data Warehouse][Authentication tooAzure SQL Data Warehouse].

<!--Articles-->
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[ADO.NET]: https://msdn.microsoft.com/library/e80y5yhx(v=vs.110).aspx
[ODBC]: https://msdn.microsoft.com/library/jj730314.aspx
[PHP]: https://msdn.microsoft.com/library/cc296172.aspx?f=255&MSPPError=-2147217396
[JDBC]: https://msdn.microsoft.com/library/mt484311(v=sql.110).aspx
[ANSI_NULLS]: https://msdn.microsoft.com/library/ms188048.aspx
[QUOTED_IDENTIFIERS]: https://msdn.microsoft.com/library/ms174393.aspx
[DATEFORMAT]: https://msdn.microsoft.com/library/ms189491.aspx
[DATEFIRST]: https://msdn.microsoft.com/library/ms181598.aspx

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->
[1]: media/sql-data-warehouse-connect-overview/get-server-name.png


