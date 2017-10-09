---
title: "VS Code: Azure SQL Veritabanında verileri bağlama ve sorgulama | Microsoft Docs"
description: "Bilgi nasıl tooconnect tooSQL veritabanına Azure üzerinde Visual Studio Code kullanarak. Ardından, Transact-SQL (T-SQL) deyimleri tooquery ve düzenleme veri çalıştırın."
metacanonical: 
keywords: "toosql veritabanına bağlanın"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 676bd799-a571-4bb8-848b-fb1720007866
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/20/2017
ms.author: carlrab
ms.openlocfilehash: ed8bdbfc3271b463a21cde5ff6b5f05fd0ff51d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-use-visual-studio-code-tooconnect-and-query-data"></a>Azure SQL Database: Kullanım Visual Studio Code tooconnect ve sorgu verileri

[Visual Studio Code](https://code.visualstudio.com/docs) Linux, macOS, grafik bir kod düzenleyicisidir ve uzantılar da dahil olmak üzere destekleyen bir Windows hello [mssql uzantısı](https://aka.ms/mssql-marketplace) Microsoft SQL Server, Azure SQL Database ve SQL Data Warehouse sorgulamak için. Bu hızlı başlangıç nasıl toouse Visual Studio Code tooconnect tooan Azure SQL veritabanı ve kullanım Transact-SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.

## <a name="prerequisites"></a>Ön koşullar

Bu hızlı başlangıç Bu hızlı başlangıçlar birinde oluşturulan başlangıç noktası hello kaynaklarını kullanır:

- [DB Oluşturma - Portal](sql-database-get-started-portal.md)
- [DB oluşturma - CLI](sql-database-get-started-cli.md)
- [DB Oluşturma - PowerShell](sql-database-get-started-powershell.md)

Başlamadan önce hello en yeni sürümünü yüklediğinizden emin olun [Visual Studio Code](https://code.visualstudio.com/Download) ve yüklenen hello [mssql uzantısı](https://aka.ms/mssql-marketplace). Merhaba mssql uzantısı için yükleme yönergeleri için bkz [yükleme VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) ve [Visual Studio Code mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

## <a name="configure-vs-code"></a>VS Code'u yapılandırma 

### <a name="mac-os"></a>**Mac OS**
MacOS için tooinstall DotNet çekirdek bu mssql uzantı kullanan bir ön koşul olan OpenSSL gerekir. Terminalinizde açın ve aşağıdaki komutları tooinstall hello girin **brew** ve **OpenSSL**. 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**

Hiçbir özel yapılandırma gerekmez.

### <a name="windows"></a>**Windows**

Hiçbir özel yapılandırma gerekmez.

## <a name="sql-server-connection-information"></a>SQL Server bağlantı bilgileri

Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure SQL veritabanı alın. Merhaba tam sunucu adını, veritabanı adının ve oturum açma bilgilerini hello sonraki yordamlarda gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası. 
3. Merhaba üzerinde **genel bakış** gözden geçirme hello veritabanınız için sayfa hello görüntü aşağıdaki gösterildiği gibi sunucu adı tam olarak nitelenmiş. Merhaba sunucu adı toobring hello yukarı üzerine getirin **tıklatın toocopy** seçeneği.

   ![bağlantı bilgileri](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Merhaba oturum açma bilgilerini Azure SQL veritabanı sunucunuz için unuttuysanız, toohello SQL veritabanı sunucusu sayfa tooview hello sunucu yönetici adı gidin ve gerekiyorsa, sıfırlama, hello parola. 

## <a name="set-language-mode-toosql"></a>Set dil modu tooSQL

Kümesi hello dil modu olarak ayarlanmış çok**SQL** Visual Studio Code tooenable mssql komutları ve T-SQL IntelliSense.

1. Yeni bir Visual Studio Code penceresi açın. 

2. Tıklatın **düz metin** hello alt sağ köşesindeki hello durum çubuğu.
3. Merhaba, **Select dil modu** açar açılır menü, türü **SQL**ve tuşuna basın **ENTER** tooset hello dil modu tooSQL. 

   ![SQL dil modu](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-tooyour-database"></a>Tooyour veritabanına bağlanın

Visual Studio Code tooestablish bağlantı tooyour Azure SQL veritabanı sunucusu kullanın.

> [!IMPORTANT]
> Devam etmeden önce sunucu, veritabanı ve oturum açma bilgilerinizin hazır olduğundan emin olun. Visual Studio koddan odağınız değiştirirseniz hello bağlantı profili bilgileri girerek başladıktan sonra hello bağlantı profili oluşturma toorestart sahip.
>

1. VS Code'da basın **CTRL + SHIFT + P** (veya **F1**) tooopen hello komutu palet.

2. **sqlcon** yazıp **ENTER** tuşuna basın.

3. Tuşuna **ENTER** tooselect **bağlantı profili oluştur**. Bu işlem, SQL Server örneğiniz için bir bağlantı profili oluşturur.

4. Merhaba yeni bağlantı profili için Hello istemleri toospecify hello bağlantı özelliklerini izleyin. Her değer belirttikten sonra basın **ENTER** toocontinue. 

   | Ayar       | Önerilen değer | Açıklama |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Sunucu adı | Merhaba tam sunucu adı | Merhaba adı şöyle olmalıdır: **mynewserver20170313.database.windows.net**. |
   | **Veritabanı adı** | mySampleDatabase | Merhaba veritabanı toowhich tooconnect Hello adı. |
   | **Kimlik doğrulaması** | SQL Oturum Açma| SQL kimlik doğrulaması biz Bu öğreticide yapılandırdığınız hello yalnızca kimlik doğrulaması türüdür. |
   | **Kullanıcı adı** | Merhaba server yönetici hesabı | Bu hello sunucu oluşturduğunuzda, belirttiğiniz hello hesabıdır. |
   | **Parola (SQL Oturum Açma)** | Sunucu yönetici hesabınız için Hello parola | Bu hello sunucu oluşturduğunuzda, belirttiğiniz hello paroladır. |
   | **Parola kaydedilsin mi?** | Evet veya Hayır | Her zaman tooenter hello parola istemiyorsanız Evet'i seçin. |
   | **Bu profil için bir ad girin** | **mySampleDatabase** gibi bir profil adı | Profil adını kaydetmek, sonraki oturum açma işlemlerinizde daha hızlı bağlantı kurmanızı sağlar. | 

5. Tuşuna hello **ESC** hello profili oluşturulur ve bağlı olduğunu bildiren anahtar tooclose hello bilgi iletisi.

6. Merhaba Durum Çubuğu'nda bağlantınızı doğrulayın.

   ![Bağlantı durumu](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a>Verileri sorgulama

Kullanım hello aşağıdaki kod tooquery hello ilk 20 ürünleri için hello kullanarak kategoriye göre [seçin](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL deyimi.

1. Merhaba, **Düzenleyicisi** penceresinde hello sorgu hello boş sorgu penceresinde aşağıdaki girin:

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. Tuşuna **CTRL + SHIFT + E** hello ürün ve ProductCategory tablolarındaki tooretrieve verileri.

    ![Sorgu](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a>Veri ekleme

Kullanım hello aşağıdaki hello SalesLT.Product tabloya hello kullanarak yeni bir ürün tooinsert kod [Ekle](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL deyimi.

1. Merhaba, **Düzenleyicisi** penceresinde hello önceki sorguyu silmek ve sorgu aşağıdaki hello girin:

   ```sql
   INSERT INTO [SalesLT].[Product]
           ( [Name]
           , [ProductNumber]
           , [Color]
           , [ProductCategoryID]
           , [StandardCost]
           , [ListPrice]
           , [SellStartDate]
           )
     VALUES
           ('myNewProduct'
           ,123456789
           ,'NewColor'
           ,1
           ,100
           ,100
           ,GETDATE() );
   ```

2. Tuşuna **CTRL + SHIFT + E** tooinsert hello ürün tablosunda yeni bir satır.

## <a name="update-data"></a>Verileri güncelleştirme

Kullanım hello aşağıdaki kod tooupdate hello yeni ürün hello kullanarak daha önce eklediğiniz [güncelleştirme](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL deyimi.

1.  Merhaba, **Düzenleyicisi** penceresinde hello önceki sorguyu silmek ve sorgu aşağıdaki hello girin:

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. Tuşuna **CTRL + SHIFT + E** hello ürün tablosundaki tooupdate hello belirtilen satır.

## <a name="delete-data"></a>Verileri silme

Kullanım hello aşağıdaki kod toodelete hello yeni ürün hello kullanarak daha önce eklediğiniz [silmek](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL deyimi.

1. Merhaba, **Düzenleyicisi** penceresinde hello önceki sorguyu silmek ve sorgu aşağıdaki hello girin:

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. Tuşuna **CTRL + SHIFT + E** hello ürün tablosundaki toodelete hello belirtilen satır.

## <a name="next-steps"></a>Sonraki adımlar

- bkz: tooconnect ve SQL Server Management Studio kullanarak sorgu [bağlanma ve sorgu SSMS ile](sql-database-connect-query-ssms.md).
- Visual Studio Code'u kullanmaya ilişkin MSDN dergisi makalesi için bkz. [MSSQL uzantısı blog gönderisinden yararlanarak veritabanı IDE'si oluşturma](https://msdn.microsoft.com/magazine/mt809115).
