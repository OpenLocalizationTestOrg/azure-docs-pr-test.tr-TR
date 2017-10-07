---
title: "MySQL çalışma ekranı MySQL'den için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç hello adımları toouse MySQL çalışma ekranı MySQL için Azure veritabanındaki tooconnect ve sorgu verileri sağlar."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a><span data-ttu-id="2feaa-103">Azure veritabanı için MySQL: kullanım MySQL çalışma ekranı tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="2feaa-103">Azure Database for MySQL: Use MySQL Workbench tooconnect and query data</span></span>
<span data-ttu-id="2feaa-104">Bu hızlı başlangıç gösteren nasıl MySQL kullanma tooconnect tooan Azure veritabanı hello MySQL çalışma ekranı uygulama.</span><span class="sxs-lookup"><span data-stu-id="2feaa-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using hello MySQL Workbench application.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2feaa-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2feaa-105">Prerequisites</span></span>
<span data-ttu-id="2feaa-106">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="2feaa-106">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2feaa-107">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2feaa-107">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="2feaa-108">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2feaa-108">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a><span data-ttu-id="2feaa-109">MySQL çalışma ekranı yükleyin</span><span class="sxs-lookup"><span data-stu-id="2feaa-109">Install MySQL Workbench</span></span>
<span data-ttu-id="2feaa-110">Karşıdan yükleyip MySQL çalışma ekranı bilgisayarınıza [hello MySQL Web sitesi](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="2feaa-110">Download and install MySQL Workbench on your computer from [hello MySQL website](https://dev.mysql.com/downloads/workbench/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="2feaa-111">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="2feaa-111">Get connection information</span></span>
<span data-ttu-id="2feaa-112">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın.</span><span class="sxs-lookup"><span data-stu-id="2feaa-112">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="2feaa-113">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="2feaa-113">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2feaa-114">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2feaa-114">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="2feaa-115">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="2feaa-115">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>

3. <span data-ttu-id="2feaa-116">Merhaba sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2feaa-116">Click hello server name.</span></span>

4. <span data-ttu-id="2feaa-117">Select hello sunucunun **özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="2feaa-117">Select hello server's **Properties** page.</span></span> <span data-ttu-id="2feaa-118">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="2feaa-118">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Azure veritabanı için MySQL sunucu adı](./media/connect-workbench/1-server-properties-name-login.png)
 
5. <span data-ttu-id="2feaa-120">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="2feaa-120">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-toohello-server-using-mysql-workbench"></a><span data-ttu-id="2feaa-121">MySQL çalışma ekranı kullanarak toohello sunucusuna bağlan</span><span class="sxs-lookup"><span data-stu-id="2feaa-121">Connect toohello server using MySQL Workbench</span></span> 
<span data-ttu-id="2feaa-122">tooconnect tooAzure MySQL server: Hello GUI aracıyla MySQL çalışma ekranı</span><span class="sxs-lookup"><span data-stu-id="2feaa-122">tooconnect tooAzure MySQL server using hello GUI tool MySQL Workbench:</span></span>

1.  <span data-ttu-id="2feaa-123">Merhaba, bilgisayarınızdaki MySQL çalışma ekranı uygulama başlatın.</span><span class="sxs-lookup"><span data-stu-id="2feaa-123">Launch hello MySQL Workbench application on your computer.</span></span> 

2.  <span data-ttu-id="2feaa-124">İçinde **yeni bağlantı kurma** iletişim kutusunda, üzerinde hello bilgisinden hello girin **parametreleri** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="2feaa-124">In **Setup New Connection** dialog box, enter hello following information on hello **Parameters** tab:</span></span>

    ![yeni bağlantı oluştur](./media/connect-workbench/2-setup-new-connection.png)

    | <span data-ttu-id="2feaa-126">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="2feaa-126">**Setting**</span></span> | <span data-ttu-id="2feaa-127">**Önerilen değer**</span><span class="sxs-lookup"><span data-stu-id="2feaa-127">**Suggested value**</span></span> | <span data-ttu-id="2feaa-128">**Alan açıklaması**</span><span class="sxs-lookup"><span data-stu-id="2feaa-128">**Field description**</span></span> |
    |---|---|---|
    |   <span data-ttu-id="2feaa-129">Bağlantı Adı</span><span class="sxs-lookup"><span data-stu-id="2feaa-129">Connection Name</span></span> | <span data-ttu-id="2feaa-130">Tanıtım Bağlantısı</span><span class="sxs-lookup"><span data-stu-id="2feaa-130">Demo Connection</span></span> | <span data-ttu-id="2feaa-131">Bu bağlantı için bir etiket belirtin.</span><span class="sxs-lookup"><span data-stu-id="2feaa-131">Specify a label for this connection.</span></span> |
    | <span data-ttu-id="2feaa-132">Bağlantı Yöntemi</span><span class="sxs-lookup"><span data-stu-id="2feaa-132">Connection Method</span></span> | <span data-ttu-id="2feaa-133">Standart (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="2feaa-133">Standard (TCP/IP)</span></span> | <span data-ttu-id="2feaa-134">Standart (TCP/IP) yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="2feaa-134">Standard (TCP/IP) is sufficient.</span></span> |
    | <span data-ttu-id="2feaa-135">Ana Bilgisayar Adı</span><span class="sxs-lookup"><span data-stu-id="2feaa-135">Hostname</span></span> | <span data-ttu-id="2feaa-136">*sunucu adı*</span><span class="sxs-lookup"><span data-stu-id="2feaa-136">*server name*</span></span> | <span data-ttu-id="2feaa-137">Hello Azure veritabanı için MySQL daha önce oluşturduğunuz zaman, kullanılan hello sunucu adı değeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="2feaa-137">Specify hello server name value that was used when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="2feaa-138">Gösterilen örnek sunucumuz: myserver4demo.mysql.database.azure.com. Merhaba tam etki alanı adını kullan (\*. mysql.database.azure.com) hello örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="2feaa-138">Our example server shown is myserver4demo.mysql.database.azure.com. Use hello fully qualified domain name (\*.mysql.database.azure.com) as shown in hello example.</span></span> <span data-ttu-id="2feaa-139">Sunucu adınız anımsamıyorsanız hello önceki bölümde tooget hello bağlantı bilgilerini hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2feaa-139">Follow hello steps in hello previous section tooget hello connection information if you do not remember your server name.</span></span>  |
    | <span data-ttu-id="2feaa-140">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="2feaa-140">Port</span></span> | <span data-ttu-id="2feaa-141">3306</span><span class="sxs-lookup"><span data-stu-id="2feaa-141">3306</span></span> | <span data-ttu-id="2feaa-142">Her zaman bağlantı noktası tooAzure veritabanı için MySQL bağlanırken 3306 kullanın.</span><span class="sxs-lookup"><span data-stu-id="2feaa-142">Always use port 3306 when connecting tooAzure Database for MySQL.</span></span> |
    | <span data-ttu-id="2feaa-143">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="2feaa-143">Username</span></span> |  <span data-ttu-id="2feaa-144">*sunucu yöneticisi oturum açma adı*</span><span class="sxs-lookup"><span data-stu-id="2feaa-144">*server admin login name*</span></span> | <span data-ttu-id="2feaa-145">İçinde hello sunucu yönetici oturum açma kullanıcı hello Azure veritabanı için MySQL daha önce oluşturduğunuz zaman sağlanan yazın.</span><span class="sxs-lookup"><span data-stu-id="2feaa-145">Type in hello server admin login username supplied when you created hello Azure Database for MySQL earlier.</span></span> <span data-ttu-id="2feaa-146">Bizim örnek kullanıcı adımız myadmin@myserver4demo.</span><span class="sxs-lookup"><span data-stu-id="2feaa-146">Our example username is myadmin@myserver4demo.</span></span> <span data-ttu-id="2feaa-147">Merhaba kullanıcıadı anımsamıyorsanız hello önceki bölümde tooget hello bağlantı bilgilerini hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2feaa-147">Follow hello steps in hello previous section tooget hello connection information if you do not remember hello username.</span></span> <span data-ttu-id="2feaa-148">Merhaba biçimi  *username@servername* .</span><span class="sxs-lookup"><span data-stu-id="2feaa-148">hello format is *username@servername*.</span></span>
    | <span data-ttu-id="2feaa-149">Parola</span><span class="sxs-lookup"><span data-stu-id="2feaa-149">Password</span></span> | <span data-ttu-id="2feaa-150">parolanız</span><span class="sxs-lookup"><span data-stu-id="2feaa-150">your password</span></span> | <span data-ttu-id="2feaa-151">Tıklatın **kasası deposunda...**  düğmesi toosave hello parola.</span><span class="sxs-lookup"><span data-stu-id="2feaa-151">Click **Store in Vault...** button toosave hello password.</span></span> |

3.   <span data-ttu-id="2feaa-152">Tıklatın **Bağlantıyı Sına** tüm parametrelerin doğru yapılandırılmışsa tootest.</span><span class="sxs-lookup"><span data-stu-id="2feaa-152">Click **Test Connection** tootest if all parameters are correctly configured.</span></span> 

4.   <span data-ttu-id="2feaa-153">Tıklatın **Tamam** toosave hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="2feaa-153">Click **OK** toosave hello connection.</span></span> 

5.   <span data-ttu-id="2feaa-154">Merhaba listesi içinde **MySQL bağlantısı**hello döşeme karşılık gelen tooyour server'ı tıklatın ve kurulan hello bağlantı toobe için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2feaa-154">In hello listing of **MySQL Connections**, click hello tile corresponding tooyour server and wait for hello connection toobe established.</span></span>

6.   <span data-ttu-id="2feaa-155">Yeni bir SQL sekmesi sorgularınızı yazabileceğiniz için boş bir Düzenleyicisi açılır.</span><span class="sxs-lookup"><span data-stu-id="2feaa-155">A new SQL tab opens with a blank editor where you can type your queries.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2feaa-156">Varsayılan olarak, SSL bağlantı güvenliği gereklidir ve Azure veritabanınızı MySQL sunucusu için zorunlu tutulur.</span><span class="sxs-lookup"><span data-stu-id="2feaa-156">By default, SSL connection security is required and enforced on your Azure Database for MySQL server.</span></span> <span data-ttu-id="2feaa-157">Genellikle SSL sertifikalarıyla ek yapılandırma MySQL çalışma ekranı tooconnect tooyour sunucusu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2feaa-157">Typically no additional configuration with SSL certificates is required for MySQL Workbench tooconnect tooyour server.</span></span> <span data-ttu-id="2feaa-158">SSL hakkında daha fazla bilgi için bkz: [yapılandırma SSL bağlantısı'nda uygulama toosecurely bağlanmak tooAzure veritabanı için MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="2feaa-158">For more information on SSL, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>  <span data-ttu-id="2feaa-159">Toodisable SSL gerekiyorsa, hello Azure portalını ziyaret edin ve hello bağlantı güvenlik sayfası toodisable hello Zorla SSL bağlantısı Değiştir düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2feaa-159">If you need toodisable SSL, visit hello Azure portal and click hello Connection security page toodisable hello Enforce SSL connection toggle button.</span></span>

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a><span data-ttu-id="2feaa-160">Bir tablo oluşturma, veri eklemek, veri okuma, verileri güncelleştirmek, verilerini sil</span><span class="sxs-lookup"><span data-stu-id="2feaa-160">Create a table, insert data, read data, update data, delete data</span></span>
1. <span data-ttu-id="2feaa-161">Merhaba örnek SQL kodu kopyalayıp boş bir SQL sekmesi tooillustrate bazı örnek veriler yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="2feaa-161">Copy and paste hello sample SQL code into a blank SQL tab tooillustrate some sample data.</span></span>

    <span data-ttu-id="2feaa-162">Bu kod quickstartdb adlı boş bir veritabanı oluşturur ve stok adlandırılmış bir örnek tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2feaa-162">This code creates an empty database named quickstartdb, and then creates a sample table named inventory.</span></span> <span data-ttu-id="2feaa-163">Bazı satırlar ekler ve ardından hello satırları okur.</span><span class="sxs-lookup"><span data-stu-id="2feaa-163">It inserts some rows, then reads hello rows.</span></span> <span data-ttu-id="2feaa-164">Bir güncelleştirme deyimi hello verilerle değiştirir ve okuma satırları yeniden Merhaba.</span><span class="sxs-lookup"><span data-stu-id="2feaa-164">It changes hello data with an update statement, and reads hello rows again.</span></span> <span data-ttu-id="2feaa-165">Son olarak, bir satırı siler ve hello satırları yeniden okur.</span><span class="sxs-lookup"><span data-stu-id="2feaa-165">Finally it deletes a row, and reads hello rows again.</span></span>
    
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

    <span data-ttu-id="2feaa-166">çalışması bittikten sonra hello ekran SQL çalışma ekranı ve hello çıktısında hello SQL kodu örneği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="2feaa-166">hello screenshot shows an example of hello SQL code in SQL Workbench and hello output after it has been run.</span></span>
    
    ![MySQL çalışma ekranı SQL sekmesi toorun örnek SQL kodu](media/connect-workbench/3-workbench-sql-tab.png)

2. <span data-ttu-id="2feaa-168">toorun hello örnek SQL kodu tıklatın hello hello araç Cıvata simgesine gölge hello **SQL dosyası** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2feaa-168">toorun hello sample SQL Code, click hello lightening bolt icon in hello toolbar of hello **SQL File** tab.</span></span>
3. <span data-ttu-id="2feaa-169">Merhaba üç sekmeli sonuçlarında hello fark **sonuç kılavuz** hello orta bölümünde hello sayfasının.</span><span class="sxs-lookup"><span data-stu-id="2feaa-169">Notice hello three tabbed results in hello **Result Grid** section in hello middle of hello page.</span></span> 
4. <span data-ttu-id="2feaa-170">Bildirim hello **çıkış** hello sayfanın hello sonundaki listesi.</span><span class="sxs-lookup"><span data-stu-id="2feaa-170">Notice hello **Output** list at hello bottom of hello page.</span></span> <span data-ttu-id="2feaa-171">Her komut Hello durumu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2feaa-171">hello status of each command is shown.</span></span> 

<span data-ttu-id="2feaa-172">Şimdi, tooAzure veritabanı için MySQL MySQL çalışma ekranı kullanarak bağlı ve hello SQL dilini kullanarak veri sorguladınız.</span><span class="sxs-lookup"><span data-stu-id="2feaa-172">Now, you have connected tooAzure Database for MySQL using MySQL Workbench, and have queried data using hello SQL language.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2feaa-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2feaa-173">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2feaa-174">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="2feaa-174">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
