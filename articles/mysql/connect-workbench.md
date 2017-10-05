---
title: "Azure veritabanı için MySQL MySQL çalışma ekranından bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç bağlanmak ve MySQL için Azure veritabanındaki verileri sorgulamak için MySQL çalışma ekranı kullanmak için adımları sağlar."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: 20a1f31ce42abb924504c4008f85420fc49aec89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-to-connect-and-query-data"></a><span data-ttu-id="9d132-103">Azure veritabanı için MySQL: kullanım MySQL çalışma ekranı bağlanmak ve verileri sorgulamak için</span><span class="sxs-lookup"><span data-stu-id="9d132-103">Azure Database for MySQL: Use MySQL Workbench to connect and query data</span></span>
<span data-ttu-id="9d132-104">Bu Hızlı Başlangıç, MySQL çalışma ekranı uygulamayı kullanarak MySQL için bir Azure veritabanına bağlanmak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9d132-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using the MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9d132-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9d132-105">Prerequisites</span></span>
<span data-ttu-id="9d132-106">Bu hızlı başlangıçta, başlangıç noktası olarak şu kılavuzlardan birinde oluşturulan kaynaklar kullanılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="9d132-106">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="9d132-107">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d132-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="9d132-108">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d132-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="9d132-109">MySQL çalışma ekranı yükleyin</span><span class="sxs-lookup"><span data-stu-id="9d132-109">Install MySQL Workbench</span></span>
<span data-ttu-id="9d132-110">Karşıdan yükleyip MySQL çalışma ekranı bilgisayarınıza [MySQL Web sitesi](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="9d132-110">Download and install MySQL Workbench on your computer from [the MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="9d132-111">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="9d132-111">Get connection information</span></span>
<span data-ttu-id="9d132-112">MySQL için Azure Veritabanı'na bağlanmak üzere gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="9d132-112">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="9d132-113">Tam sunucu adına ve oturum açma kimlik bilgilerine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="9d132-113">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="9d132-114">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9d132-114">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="9d132-115">Azure portalında sol taraftaki menüden **Tüm kaynaklar**'a tıklayın ve oluşturduğunuz sunucuyu (örneğin, **myserver4demo**) arayın.</span><span class="sxs-lookup"><span data-stu-id="9d132-115">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="9d132-116">Sunucunun adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9d132-116">Click the server name.</span></span>

4. <span data-ttu-id="9d132-117">Sunucunun **Özellikler** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="9d132-117">Select the server's **Properties** page.</span></span> <span data-ttu-id="9d132-118">**Sunucu adını** ve **Sunucu yöneticisi oturum açma adını** not edin.</span><span class="sxs-lookup"><span data-stu-id="9d132-118">Make a note of the **Server name** and **Server admin login name**.</span></span>

 ![Azure veritabanı için MySQL sunucu adı](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="9d132-120">Sunucunuzun oturum açma bilgilerini unuttuysanız **Genel Bakış** sayfasına giderek Sunucu yöneticisi oturum açma adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="9d132-120">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-to-the-server-using-mysql-workbench"></a><span data-ttu-id="9d132-121">MySQL çalışma ekranı kullanarak sunucuya bağlanın</span><span class="sxs-lookup"><span data-stu-id="9d132-121">Connect to the server using MySQL Workbench</span></span> 
<span data-ttu-id="9d132-122">MySQL Workbench GUI aracını kullanarak Azure MySQL sunucusuna bağlanmak için:</span><span class="sxs-lookup"><span data-stu-id="9d132-122">To connect to Azure MySQL server using the GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="9d132-123">Bilgisayarınızda MySQL çalışma ekranı uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="9d132-123">Launch the MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="9d132-124">İçinde **yeni bağlantı kurma** iletişim kutusunda, aşağıdaki bilgileri girin **parametreleri** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="9d132-124">In **Setup New Connection** dialog box, enter the following information on the **Parameters** tab:</span></span>

    ![yeni bağlantı oluştur](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="9d132-126">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="9d132-126">**Setting**</span></span> | <span data-ttu-id="9d132-127">**Önerilen değer**</span><span class="sxs-lookup"><span data-stu-id="9d132-127">**Suggested value**</span></span> | <span data-ttu-id="9d132-128">**Alan açıklaması**</span><span class="sxs-lookup"><span data-stu-id="9d132-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="9d132-129">Bağlantı Adı</span><span class="sxs-lookup"><span data-stu-id="9d132-129">Connection Name</span></span> | <span data-ttu-id="9d132-130">Tanıtım Bağlantısı</span><span class="sxs-lookup"><span data-stu-id="9d132-130">Demo Connection</span></span> | <span data-ttu-id="9d132-131">Bu bağlantı için bir etiket belirtin.</span><span class="sxs-lookup"><span data-stu-id="9d132-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="9d132-132">Bağlantı Yöntemi</span><span class="sxs-lookup"><span data-stu-id="9d132-132">Connection Method</span></span> | <span data-ttu-id="9d132-133">Standart (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="9d132-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="9d132-134">Standart (TCP/IP) yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="9d132-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="9d132-135">Ana Bilgisayar Adı</span><span class="sxs-lookup"><span data-stu-id="9d132-135">Hostname</span></span> | <span data-ttu-id="9d132-136">*sunucu adı*</span><span class="sxs-lookup"><span data-stu-id="9d132-136">*server name*</span></span> | <span data-ttu-id="9d132-137">MySQL için Azure Veritabanını oluştururken kullandığınız sunucu adı değerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="9d132-137">Specify the server name value that was used when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="9d132-138">Gösterilen örnek sunucumuz: myserver4demo.mysql.database.azure.com. Örnekte gösterildiği gibi tam etki alanı adını (\*.mysql.database.azure.com) kullanın.</span><span class="sxs-lookup"><span data-stu-id="9d132-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use the fully qualified domain name (\*.mysql.database.azure.com) as shown in the example.</span></span> <span data-ttu-id="9d132-139">Sunucu adınızı anımsamıyorsanız bağlantı bilgilerini almak için bir önceki bölümdeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="9d132-139">Follow the steps in the previous section to get the connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="9d132-140">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="9d132-140">Port</span></span> | <span data-ttu-id="9d132-141">3306</span><span class="sxs-lookup"><span data-stu-id="9d132-141">3306</span></span> | <span data-ttu-id="9d132-142">MySQL Azure veritabanına bağlanırken her zaman bağlantı noktası olarak 3306 kullanın.</span><span class="sxs-lookup"><span data-stu-id="9d132-142">Always use port 3306 when connecting to Azure Database for MySQL.</span></span> |
    | <span data-ttu-id="9d132-143">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="9d132-143">Username</span></span> |  <span data-ttu-id="9d132-144">*sunucu yöneticisi oturum açma adı*</span><span class="sxs-lookup"><span data-stu-id="9d132-144">*server admin login name*</span></span> | <span data-ttu-id="9d132-145">MySQL için Azure Veritabanını oluştururken girdiğiniz sunucu yöneticisi oturum açma kullanıcı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="9d132-145">Type in the server admin login username supplied when you created the Azure Database for MySQL earlier.</span></span> <span data-ttu-id="9d132-146">Bizim örnek kullanıcı adımız myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="9d132-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="9d132-147">Kullanıcı adını anımsamıyorsanız bağlantı bilgilerini almak için bir önceki bölümdeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="9d132-147">Follow the steps in the previous section to get the connection information if you do not remember the username.</span></span> <span data-ttu-id="9d132-148">Biçim şöyledir: *username@servername*.</span><span class="sxs-lookup"><span data-stu-id="9d132-148">The format is *username@servername*.</span></span>
    | <span data-ttu-id="9d132-149">Parola</span><span class="sxs-lookup"><span data-stu-id="9d132-149">Password</span></span> | <span data-ttu-id="9d132-150">parolanız</span><span class="sxs-lookup"><span data-stu-id="9d132-150">your password</span></span> | <span data-ttu-id="9d132-151">Tıklatın **kasası deposunda...**  Parolayı Kaydet düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9d132-151">Click **Store in Vault...** button to save the password.</span></span> |

3.   <span data-ttu-id="9d132-152">Tüm parametrelerin doğru yapılandırılıp yapılandırılmadığını test etmek için **Bağlantıyı Sına**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9d132-152">Click **Test Connection** to test if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="9d132-153">Tıklatın **Tamam** bağlantıyı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="9d132-153">Click **OK** to save the connection.</span></span> 

5.   <span data-ttu-id="9d132-154">Listesini içinde **MySQL bağlantısı**, sunucunuza karşılık gelen kutucuğa tıklayın ve bağlantının sağlanabilmesi için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="9d132-154">In the listing of **MySQL Connections**, click the tile corresponding to your server and wait for the connection to be established.</span></span>

6.   <span data-ttu-id="9d132-155">Yeni bir SQL sekmesi sorgularınızı yazabileceğiniz için boş bir Düzenleyicisi açılır.</span><span class="sxs-lookup"><span data-stu-id="9d132-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9d132-156">Varsayılan olarak, SSL bağlantı güvenliği gereklidir ve Azure veritabanınızı MySQL sunucusu için zorunlu tutulur.</span><span class="sxs-lookup"><span data-stu-id="9d132-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="9d132-157">Genellikle SSL sertifikalarıyla ek yapılandırma MySQL sunucunuza bağlanmak çalışma ekranı için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9d132-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench to connect to your server.</span></span> <span data-ttu-id="9d132-158">SSL hakkında daha fazla bilgi için bkz: [uygulamanızda güvenli bir şekilde MySQL için Azure veritabanına bağlanmak için SSL yapılandırma bağlantısı](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="9d132-158">For more information on SSL, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="9d132-159">SSL devre dışı bırakmanız gerekirse Azure portalını ziyaret edin ve zorunlu SSL bağlantısı iki durumlu düğme devre dışı bırakmak için bağlantı güvenliği Sayfası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9d132-159">If you need to disable SSL, visit the Azure portal and click the Connection security page to disable the Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="9d132-160">Bir tablo oluşturma, veri eklemek, veri okuma, verileri güncelleştirmek, verilerini sil</span><span class="sxs-lookup"><span data-stu-id="9d132-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="9d132-161">Örnek SQL kodu kopyalayıp bazı örnek veriler göstermek için boş bir SQL sekmesi yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="9d132-161">Copy and paste the sample SQL code into a blank SQL tab to illustrate some sample data.</span></span>

    <span data-ttu-id="9d132-162">Bu kod quickstartdb adlı boş bir veritabanı oluşturur ve stok adlandırılmış bir örnek tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9d132-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="9d132-163">Bazı satırlar ekler satırları daha sonra okur.</span><span class="sxs-lookup"><span data-stu-id="9d132-163">It inserts some rows, then reads the rows.</span></span> <span data-ttu-id="9d132-164">Bir güncelleştirme deyimi verilerle değiştirir ve satırları yeniden okur.</span><span class="sxs-lookup"><span data-stu-id="9d132-164">It changes the data with an update statement, and reads the rows again.</span></span> <span data-ttu-id="9d132-165">Son olarak, bir satır siler ve satırları yeniden okur.</span><span class="sxs-lookup"><span data-stu-id="9d132-165">Finally it deletes a row, and reads the rows again.</span></span>
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    <span data-ttu-id="9d132-166">Çalışması bittikten sonra ekran SQL çalışma ekranı hem de çıkış SQL kod örneğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9d132-166">The screenshot shows an example of the SQL code in SQL Workbench and the output after it has been run.</span></span>
    
    ![Örnek SQL kodu çalıştırmak için MySQL çalışma ekranı SQL sekmesi](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="9d132-168">SQL kodu örneği çalıştırmak için araç çubuğunda açıklaştırıcı Cıvata simgesini tıklatın **SQL dosyası** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9d132-168">To run the sample SQL Code, click the lightening bolt icon in the toolbar of the **SQL File** tab.</span></span>
3. <span data-ttu-id="9d132-169">Üç sekmeli sonuçlarında fark **sonuç kılavuz** sayfasının ortasında bölümü.</span><span class="sxs-lookup"><span data-stu-id="9d132-169">Notice the three tabbed results in the **Result Grid** section in the middle of the page.</span></span> 
4. <span data-ttu-id="9d132-170">Bildirim **çıkış** sayfanın sonundaki listesi.</span><span class="sxs-lookup"><span data-stu-id="9d132-170">Notice the **Output** list at the bottom of the page.</span></span> <span data-ttu-id="9d132-171">Her komut durumu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9d132-171">The status of each command is shown.</span></span> 

<span data-ttu-id="9d132-172">Şimdi, Azure veritabanı için MySQL çalışma ekranı kullanarak MySQL için bağlı ve SQL dilini kullanarak veri sorguladınız.</span><span class="sxs-lookup"><span data-stu-id="9d132-172">Now, you have connected to Azure Database for MySQL using MySQL Workbench, and have queried data using the SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d132-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9d132-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9d132-174">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="9d132-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
