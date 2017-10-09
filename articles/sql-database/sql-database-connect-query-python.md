---
title: "aaaUse Python tooquery Azure SQL veritabanı | Microsoft Docs"
description: "Bu konu, nasıl gösterir toouse Python toocreate tooan Azure SQL veritabanı ve sorgu Transact-SQL deyimi kullanarak bağlanan bir program."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a>Python tooquery Azure SQL veritabanını kullan

 Bu hızlı başlangıç gösteren nasıl toouse [Python](https://python.org) tooconnect tooan Azure SQL veritabanı ve Transact-SQL deyimleri tooquery verileri kullanın.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu hızlı başlangıç Öğreticisi, hello aşağıdaki sahip olduğunuzdan emin olun:

- Bir Azure SQL veritabanı. Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan hello kaynakları kullanır: 

   - [DB Oluşturma - Portal](sql-database-get-started-portal.md)
   - [DB oluşturma - CLI](sql-database-get-started-cli.md)
   - [DB Oluşturma - PowerShell](sql-database-get-started-powershell.md)

- A [sunucu düzeyinde güvenlik duvarı kuralı](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) hello için genel IP adresi hello bilgisayarın bu hızlı başlangıç öğreticisi için kullanın.

- İşletim sisteminiz için Python ve ilgili yazılımları yüklediniz.

    - **MacOS**: Homebrew yükleyin ve Python hello ODBC sürücüsü ve SQLCMD yükleyin ve SQL Server için hello Python sürücü yükleyin. Bkz. [Adım 1.2, 1.3 ve 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).
    - **Ubuntu**: Python yüklemek ve diğer SQL Server için gerekli paketleri ve yükleme hello Python sürücü. Bkz. [Adım 1.2, 1.3 ve 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).
    - **Windows**: hello (ortam değişkeni yapılandırılmış sizin için) Python en yeni sürümünü yüklemek için hello ODBC sürücüsü ve SQLCMD yükleyin ve SQL Server için hello Python sürücü yükleyin. Bkz: [1.2, 1.3 ve 2.1 adımları](https://www.microsoft.com/sql-server/developer-get-started/python/windows/). 

## <a name="sql-server-connection-information"></a>SQL Server bağlantı bilgileri

Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın. Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası. 
3. Merhaba üzerinde **genel bakış** gözden geçirme hello veritabanınız için sayfa hello görüntü aşağıdaki gösterildiği gibi sunucu adı tam olarak nitelenmiş. Merhaba sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Sunucu oturum açma bilgilerinizi unutursanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin ve gerekiyorsa, sıfırlama, hello parola.     
    
## <a name="insert-code-tooquery-sql-database"></a>Kod tooquery SQL veritabanı Ekle 

1. Sık kullandığınız metin düzenleyicisinde **sqltest.py** adında yeni bir dosya oluşturun.  

2. Aşağıdaki kod ve sunucu, veritabanı, kullanıcı ve parola için uygun değerleri hello ekleme hello Hello içeriğini değiştirin.

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a>Merhaba kodu çalıştırma

1. Merhaba komut isteminde aşağıdaki komutları hello çalıştırın:

   ```Python
   python sqltest.py
   ```

2. Merhaba üst 20 satır döndürülür ve hello uygulama penceresini kapatın doğrulayın.

## <a name="next-steps"></a>Sonraki adımlar

- [İlk Azure SQL veritabanınızı tasarlama](sql-database-design-first-database.md)
- [SQL Server için Microsoft Python Sürücüleri](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [Python Geliştirici Merkezi](https://azure.microsoft.com/develop/python/?v=17.23h)

