---
title: "VS Code: Azure SQL Veritabanında verileri bağlama ve sorgulama | Microsoft Docs"
description: "Visual Studio Code kullanarak SQL Veritabanına bağlanma hakkında bilgi edinin. Ardından, verileri sorgulamak ve düzenlemek için Transact-SQL (T-SQL) deyimleri çalıştırın."
metacanonical: 
keywords: "sql veritabanına bağlanma"
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
ms.openlocfilehash: 4076b1e7ab3a70009217a1deff72da4bff0dc871
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sql-database-use-visual-studio-code-to-connect-and-query-data"></a><span data-ttu-id="7105c-105">Azure SQL Veritabanı: Visual Studio Code kullanarak verileri bağlama ve sorgulama</span><span class="sxs-lookup"><span data-stu-id="7105c-105">Azure SQL Database: Use Visual Studio Code to connect and query data</span></span>

<span data-ttu-id="7105c-106">Linux, macOS ve Windows’a yönelik bir grafik kod düzenleyicisi olan [Visual Studio Code](https://code.visualstudio.com/docs); Microsoft SQL Server, Azure SQL Veritabanı ve SQL Veri Ambarı’nı sorgulamak için kullanılabilen [mssql uzantısı](https://aka.ms/mssql-marketplace) gibi uzantıları destekler.</span><span class="sxs-lookup"><span data-stu-id="7105c-106">[Visual Studio Code](https://code.visualstudio.com/docs) is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="7105c-107">Bu hızlı başlangıçta Visual Studio Code’u kullanarak bir Azure SQL veritabanına bağlanma ve daha sonra Transact-SQL deyimlerini kullanarak veritabanındaki verileri sorgulama, ekleme, güncelleştirme ve silme işlemlerinin nasıl yapılacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="7105c-107">This quick start demonstrates how to use Visual Studio Code to connect to an Azure SQL database, and then use Transact-SQL statements to query, insert, update, and delete data in the database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7105c-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7105c-108">Prerequisites</span></span>

<span data-ttu-id="7105c-109">Bu hızlı başlangıçta başlangıç noktası olarak bu hızlı başlangıçlardan birinde oluşturulan kaynaklar kullanılır:</span><span class="sxs-lookup"><span data-stu-id="7105c-109">This quick start uses as its starting point the resources created in one of these quick starts:</span></span>

- [<span data-ttu-id="7105c-110">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="7105c-110">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
- [<span data-ttu-id="7105c-111">DB oluşturma - CLI</span><span class="sxs-lookup"><span data-stu-id="7105c-111">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
- [<span data-ttu-id="7105c-112">DB Oluşturma - PowerShell</span><span class="sxs-lookup"><span data-stu-id="7105c-112">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

<span data-ttu-id="7105c-113">Başlamadan önce en yeni [Visual Studio Code](https://code.visualstudio.com/Download) sürümünü yüklediğinizden [mssql uzantısının](https://aka.ms/mssql-marketplace) yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7105c-113">Before you start, make sure you have installed the newest version of [Visual Studio Code](https://code.visualstudio.com/Download) and loaded the [mssql extension](https://aka.ms/mssql-marketplace).</span></span> <span data-ttu-id="7105c-114">mssql uzantısına ilişkin yükleme yönergeleri için bkz. [VS Code Yükleme](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) ve [Visual Studio Code için mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span><span class="sxs-lookup"><span data-stu-id="7105c-114">For installation guidance for the mssql extension, see [Install VS Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode#install-vs-code) and see [mssql for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).</span></span> 

## <a name="configure-vs-code"></a><span data-ttu-id="7105c-115">VS Code'u yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7105c-115">Configure VS Code</span></span> 

### <a name="mac-os"></a><span data-ttu-id="7105c-116">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="7105c-116">**Mac OS**</span></span>
<span data-ttu-id="7105c-117">macOS için, mssql uzantısının kullandığı DotNet Core’a yönelik bir ön koşul olan OpenSSL’yi yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7105c-117">For macOS, you need to install OpenSSL which is a prerequiste for DotNet Core that mssql extention uses.</span></span> <span data-ttu-id="7105c-118">**brew** ve **OpenSSL**’yi yüklemek için terminalinizi açın aşağıdaki komutları girin.</span><span class="sxs-lookup"><span data-stu-id="7105c-118">Open your terminal and enter the following commands to install **brew** and **OpenSSL**.</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

### <a name="linux-ubuntu"></a><span data-ttu-id="7105c-119">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="7105c-119">**Linux (Ubuntu)**</span></span>

<span data-ttu-id="7105c-120">Hiçbir özel yapılandırma gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7105c-120">No special configuration needed.</span></span>

### <a name="windows"></a><span data-ttu-id="7105c-121">**Windows**</span><span class="sxs-lookup"><span data-stu-id="7105c-121">**Windows**</span></span>

<span data-ttu-id="7105c-122">Hiçbir özel yapılandırma gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7105c-122">No special configuration needed.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="7105c-123">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="7105c-123">SQL server connection information</span></span>

<span data-ttu-id="7105c-124">Azure SQL veritabanına bağlanmak için gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="7105c-124">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="7105c-125">Sonraki yordamlarda tam sunucu adına, veritabanı adına ve oturum açma bilgilerine ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7105c-125">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="7105c-126">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7105c-126">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="7105c-127">Soldaki menüden **SQL Veritabanları**’nı seçin ve **SQL veritabanları** sayfasında veritabanınıza tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7105c-127">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="7105c-128">Veritabanınızın **Genel Bakış** sayfasında, aşağıdaki görüntüde gösterildiği gibi tam sunucu adını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="7105c-128">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="7105c-129">Sunucu adının üzerine gelerek **Kopyalamak için tıklayın** seçeneğini ortaya çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7105c-129">You can hover over the server name to bring up the **Click to copy** option.</span></span>

   ![bağlantı bilgileri](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="7105c-131">Azure SQL Veritabanı sunucunuzun oturum açma bilgilerini unuttuysanız, SQL Veritabanı sunucu sayfasına giderek sunucu yöneticisi adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="7105c-131">If you have forgotten the login information for your Azure SQL Database server, navigate to the SQL Database server page to view the server admin name and, if necessary, reset the password.</span></span> 

## <a name="set-language-mode-to-sql"></a><span data-ttu-id="7105c-132">Dili modunu SQL’e ayarlama</span><span class="sxs-lookup"><span data-stu-id="7105c-132">Set language mode to SQL</span></span>

<span data-ttu-id="7105c-133">mssql komutlarını ve T-SQL IntelliSense’i etkinleştirmek için dil modunu Visual Studio Code’da **SQL** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7105c-133">Set the language mode is set to **SQL** in Visual Studio Code to enable mssql commands and T-SQL IntelliSense.</span></span>

1. <span data-ttu-id="7105c-134">Yeni bir Visual Studio Code penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="7105c-134">Open a new Visual Studio Code window.</span></span> 

2. <span data-ttu-id="7105c-135">Durum çubuğunun sağ alt köşesindeki **Düz Metin**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7105c-135">Click **Plain Text** in the lower right-hand corner of the status bar.</span></span>
3. <span data-ttu-id="7105c-136">Görüntülenen **Dil modu seç** açılır menüsüne **SQL** yazın ve **ENTER** tuşuna basarak dil modunu SQL’e ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7105c-136">In the **Select language mode** drop-down menu that opens, type **SQL**, and then press **ENTER** to set the language mode to SQL.</span></span> 

   ![SQL dil modu](./media/sql-database-connect-query-vscode/vscode-language-mode.png)

## <a name="connect-to-your-database"></a><span data-ttu-id="7105c-138">Veritabanınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="7105c-138">Connect to your database</span></span>

<span data-ttu-id="7105c-139">Visual Studio Code’u kullanarak Azure SQL Veritabanı sunucunuzla bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="7105c-139">Use Visual Studio Code to establish a connection to your Azure SQL Database server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7105c-140">Devam etmeden önce sunucu, veritabanı ve oturum açma bilgilerinizin hazır olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7105c-140">Before continuing, make sure that you have your server, database, and login information ready.</span></span> <span data-ttu-id="7105c-141">Bağlantı profili bilgilerini girmeye başladıktan sonra, odağınızı Visual Studio Code’dan değiştirirseniz bağlantı profili oluşturma işlemini yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7105c-141">Once you begin entering the connection profile information, if you change your focus from Visual Studio Code, you have to restart creating the connection profile.</span></span>
>

1. <span data-ttu-id="7105c-142">VS Code’da **CTRL+SHIFT+P** (veya **F1**) tuşlarına basarak Komut Paletini açın.</span><span class="sxs-lookup"><span data-stu-id="7105c-142">In VS Code, press **CTRL+SHIFT+P** (or **F1**) to open the Command Palette.</span></span>

2. <span data-ttu-id="7105c-143">**sqlcon** yazıp **ENTER** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7105c-143">Type **sqlcon** and press **ENTER**.</span></span>

3. <span data-ttu-id="7105c-144">**ENTER** tuşuna basarak **Bağlantı Profili Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="7105c-144">Press **ENTER** to select **Create Connection Profile**.</span></span> <span data-ttu-id="7105c-145">Bu işlem, SQL Server örneğiniz için bir bağlantı profili oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7105c-145">This creates a connection profile for your SQL Server instance.</span></span>

4. <span data-ttu-id="7105c-146">Yeni bağlantı profilinin bağlantı özelliklerini belirtmek için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="7105c-146">Follow the prompts to specify the connection properties for the new connection profile.</span></span> <span data-ttu-id="7105c-147">Her bir değeri belirttikten sonra **ENTER** tuşuna basarak devam edin.</span><span class="sxs-lookup"><span data-stu-id="7105c-147">After specifying each value, press **ENTER** to continue.</span></span> 

   | <span data-ttu-id="7105c-148">Ayar</span><span class="sxs-lookup"><span data-stu-id="7105c-148">Setting</span></span>       | <span data-ttu-id="7105c-149">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="7105c-149">Suggested value</span></span> | <span data-ttu-id="7105c-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7105c-150">Description</span></span> |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="7105c-151">**Sunucu adı</span><span class="sxs-lookup"><span data-stu-id="7105c-151">**Server name</span></span> | <span data-ttu-id="7105c-152">Tam sunucu adı</span><span class="sxs-lookup"><span data-stu-id="7105c-152">The fully qualified server name</span></span> | <span data-ttu-id="7105c-153">Ad şunun gibi olmalıdır: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="7105c-153">The name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="7105c-154">**Veritabanı adı**</span><span class="sxs-lookup"><span data-stu-id="7105c-154">**Database name**</span></span> | <span data-ttu-id="7105c-155">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="7105c-155">mySampleDatabase</span></span> | <span data-ttu-id="7105c-156">Bağlanılacak veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="7105c-156">The name of the database to which to connect.</span></span> |
   | <span data-ttu-id="7105c-157">**Kimlik doğrulaması**</span><span class="sxs-lookup"><span data-stu-id="7105c-157">**Authentication**</span></span> | <span data-ttu-id="7105c-158">SQL Oturum Açma</span><span class="sxs-lookup"><span data-stu-id="7105c-158">SQL Login</span></span>| <span data-ttu-id="7105c-159">Bu öğreticide yapılandırdığımız tek kimlik doğrulaması türü SQL Kimlik Doğrulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="7105c-159">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="7105c-160">**Kullanıcı adı**</span><span class="sxs-lookup"><span data-stu-id="7105c-160">**User name**</span></span> | <span data-ttu-id="7105c-161">Sunucu yöneticisi hesabı</span><span class="sxs-lookup"><span data-stu-id="7105c-161">The server admin account</span></span> | <span data-ttu-id="7105c-162">Bu, sunucuyu oluştururken belirttiğiniz hesaptır.</span><span class="sxs-lookup"><span data-stu-id="7105c-162">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="7105c-163">**Parola (SQL Oturum Açma)**</span><span class="sxs-lookup"><span data-stu-id="7105c-163">**Password (SQL Login)**</span></span> | <span data-ttu-id="7105c-164">Sunucu yöneticisi hesabınızın parolası</span><span class="sxs-lookup"><span data-stu-id="7105c-164">The password for your server admin account</span></span> | <span data-ttu-id="7105c-165">Bu, sunucuyu oluştururken belirttiğiniz paroladır.</span><span class="sxs-lookup"><span data-stu-id="7105c-165">This is the password that you specified when you created the server.</span></span> |
   | <span data-ttu-id="7105c-166">**Parola kaydedilsin mi?**</span><span class="sxs-lookup"><span data-stu-id="7105c-166">**Save Password?**</span></span> | <span data-ttu-id="7105c-167">Evet veya Hayır</span><span class="sxs-lookup"><span data-stu-id="7105c-167">Yes or No</span></span> | <span data-ttu-id="7105c-168">Her defasında parolayı girmek istemiyorsanız Evet seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="7105c-168">Select Yes if you do not want to enter the password each time.</span></span> |
   | <span data-ttu-id="7105c-169">**Bu profil için bir ad girin**</span><span class="sxs-lookup"><span data-stu-id="7105c-169">**Enter a name for this profile**</span></span> | <span data-ttu-id="7105c-170">**mySampleDatabase** gibi bir profil adı</span><span class="sxs-lookup"><span data-stu-id="7105c-170">A profile name, such as **mySampleDatabase**</span></span> | <span data-ttu-id="7105c-171">Profil adını kaydetmek, sonraki oturum açma işlemlerinizde daha hızlı bağlantı kurmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7105c-171">A saved profile name speeds your connection on subsequent logins.</span></span> | 

5. <span data-ttu-id="7105c-172">Profilin oluşturulup bağlandığını bildiren bilgi iletisini kapatmak için **ESC** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7105c-172">Press the **ESC** key to close the info message that informs you that the profile is created and connected.</span></span>

6. <span data-ttu-id="7105c-173">Durum çubuğunda bağlantınızı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7105c-173">Verify your connection in the status bar.</span></span>

   ![Bağlantı durumu](./media/sql-database-connect-query-vscode/vscode-connection-status.png)

## <a name="query-data"></a><span data-ttu-id="7105c-175">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="7105c-175">Query data</span></span>

<span data-ttu-id="7105c-176">[SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL deyimini kullanarak ilk 20 ürünü kategoriye göre sorgulamak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7105c-176">Use the following code to query for the top 20 products by category using the [SELECT](https://msdn.microsoft.com/library/ms189499.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="7105c-177">**Düzenleyici** penceresinde boş sorgu penceresine aşağıdaki sorguyu girin:</span><span class="sxs-lookup"><span data-stu-id="7105c-177">In the **Editor** window, enter the following query in the empty query window:</span></span>

   ```sql
   SELECT pc.Name as CategoryName, p.name as ProductName
   FROM [SalesLT].[ProductCategory] pc
   JOIN [SalesLT].[Product] p
   ON pc.productcategoryid = p.productcategoryid;
   ```

2. <span data-ttu-id="7105c-178">**CTRL+SHIFT+E** tuşlarına basarak Product ve ProductCategory tablolarından verileri alın.</span><span class="sxs-lookup"><span data-stu-id="7105c-178">Press **CTRL+SHIFT+E** to retrieve data from the Product and ProductCategory tables.</span></span>

    ![Sorgu](./media/sql-database-connect-query-vscode/query.png)

## <a name="insert-data"></a><span data-ttu-id="7105c-180">Veri ekleme</span><span class="sxs-lookup"><span data-stu-id="7105c-180">Insert data</span></span>

<span data-ttu-id="7105c-181">[INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL deyimini kullanarak SalesLT.Product tablosuna yeni ürün eklemek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7105c-181">Use the following code to insert a new product into the SalesLT.Product table using the [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="7105c-182">**Düzenleyici** penceresinde önceki sorguyu silip aşağıdaki sorguyu girin:</span><span class="sxs-lookup"><span data-stu-id="7105c-182">In the **Editor** window, delete the previous query and enter the following query:</span></span>

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

2. <span data-ttu-id="7105c-183">Product tablosuna yeni bir satır eklemek için **CTRL+SHIFT+E** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="7105c-183">Press **CTRL+SHIFT+E** to insert a new row in the Product table.</span></span>

## <a name="update-data"></a><span data-ttu-id="7105c-184">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7105c-184">Update data</span></span>

<span data-ttu-id="7105c-185">[UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL deyimini kullanarak daha önce eklemiş olduğunuz yeni ürünü güncelleştirmek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7105c-185">Use the following code to update the new product that you previously added using the [UPDATE](https://msdn.microsoft.com/library/ms177523.aspx) Transact-SQL statement.</span></span>

1.  <span data-ttu-id="7105c-186">**Düzenleyici** penceresinde önceki sorguyu silip aşağıdaki sorguyu girin:</span><span class="sxs-lookup"><span data-stu-id="7105c-186">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   UPDATE [SalesLT].[Product]
   SET [ListPrice] = 125
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="7105c-187">Product tablosunda belirtilen satırı güncelleştirmek için **CTRL+SHIFT+E** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="7105c-187">Press **CTRL+SHIFT+E** to update the specified row in the Product table.</span></span>

## <a name="delete-data"></a><span data-ttu-id="7105c-188">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="7105c-188">Delete data</span></span>

<span data-ttu-id="7105c-189">[DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL deyimini kullanarak daha önce eklemiş olduğunuz yeni ürünü silmek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7105c-189">Use the following code to delete the new product that you previously added using the [DELETE](https://msdn.microsoft.com/library/ms189835.aspx) Transact-SQL statement.</span></span>

1. <span data-ttu-id="7105c-190">**Düzenleyici** penceresinde önceki sorguyu silip aşağıdaki sorguyu girin:</span><span class="sxs-lookup"><span data-stu-id="7105c-190">In the **Editor** window, delete the previous query and enter the following query:</span></span>

   ```sql
   DELETE FROM [SalesLT].[Product]
   WHERE Name = 'myNewProduct';
   ```

2. <span data-ttu-id="7105c-191">Product tablosunda belirtilen satırı silmek için **CTRL+SHIFT+E** tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="7105c-191">Press **CTRL+SHIFT+E** to delete the specified row in the Product table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7105c-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7105c-192">Next steps</span></span>

- <span data-ttu-id="7105c-193">SQL Server Management Studio kullanarak bağlanmak ve sorgu yürütmek için bkz. [SSMS ile bağlanma ve sorgu yürütme](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="7105c-193">To connect and query using SQL Server Management Studio, see [Connect and query with SSMS](sql-database-connect-query-ssms.md).</span></span>
- <span data-ttu-id="7105c-194">Visual Studio Code'u kullanmaya ilişkin MSDN dergisi makalesi için bkz. [MSSQL uzantısı blog gönderisinden yararlanarak veritabanı IDE'si oluşturma](https://msdn.microsoft.com/magazine/mt809115).</span><span class="sxs-lookup"><span data-stu-id="7105c-194">For an MSDN magazine article on using Visual Studio Code, see [Create a database IDE with MSSQL extension blog post](https://msdn.microsoft.com/magazine/mt809115).</span></span>
