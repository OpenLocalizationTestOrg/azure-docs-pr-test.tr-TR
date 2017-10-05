---
title: "C++'tan MySQL için Azure Veritabanı'na bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıçta, MySQL için Azure Veritabanı'na bağlanmak ve buradan veri sorgulamak için kullanabileceğiniz bir C++ kod örneği sağlanmıştır."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: 63388b83b913d95136140fa4c56af0dbebbdad81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-database-for-mysql-use-connectorc-to-connect-and-query-data"></a><span data-ttu-id="b1b94-103">MySQL için Azure Veritabanı: Connector/C++ kullanarak bağlanma ve veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="b1b94-103">Azure Database for MySQL: Use Connector/C++ to connect and query data</span></span>
<span data-ttu-id="b1b94-104">Bu hızlı başlangıçta C++ uygulaması kullanarak MySQL için Azure Veritabanı'na nasıl bağlanacağınız gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b1b94-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="b1b94-105">Ayrıca veritabanında veri sorgulamak, eklemek, güncelleştirmek ve silmek için SQL deyimlerini nasıl kullanacağınız da gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b1b94-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="b1b94-106">Bu makaledeki adımlarda, C++ kullanarak geliştirmeyle ilgili bilgi sahibi olduğunuz ve MySQL için Azure Veritabanı ile çalışmaya yeni başladığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-106">The steps in this article assume that you are familiar with developing using C++, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1b94-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b1b94-107">Prerequisites</span></span>
<span data-ttu-id="b1b94-108">Bu hızlı başlangıçta, başlangıç noktası olarak şu kılavuzlardan birinde oluşturulan kaynaklar kullanılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="b1b94-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="b1b94-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1b94-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="b1b94-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1b94-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="b1b94-111">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b1b94-111">You also need to:</span></span>
- <span data-ttu-id="b1b94-112">[.Net Framework](https://www.microsoft.com/net/download)'ü yükleme</span><span class="sxs-lookup"><span data-stu-id="b1b94-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="b1b94-113">[Visual Studio](https://www.visualstudio.com/downloads/)'yu yükleme</span><span class="sxs-lookup"><span data-stu-id="b1b94-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="b1b94-114">[MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/) yükleyin</span><span class="sxs-lookup"><span data-stu-id="b1b94-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="b1b94-115">[Boost](http://www.boost.org/)’u yükleyin</span><span class="sxs-lookup"><span data-stu-id="b1b94-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="b1b94-116">Visual Studio'yu ve .NET'i yükleme</span><span class="sxs-lookup"><span data-stu-id="b1b94-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="b1b94-117">Bu bölümdeki adımlarda .NET kullanarak geliştirmeyle ilgili bilgi sahibi olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-117">The steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="b1b94-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="b1b94-118">**Windows**</span></span>
1. <span data-ttu-id="b1b94-119">Android, iOS ve Windows’un yanı sıra web ve veritabanı uygulamaları ile bulut hizmetleri için modern uygulamalar oluşturmaya yönelik tam özellikli, genişletilebilir, ücretsiz bir IDE olan Visual Studio 2017 Community’yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b1b94-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="b1b94-120">.NET Framework’ün tamamını ya da yalnızca .NET Core’u yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1b94-120">You can install either the full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="b1b94-121">Hızlı başlangıçtaki kod parçacıkları her ikisiyle de çalışır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-121">The code snippets in the Quickstart work with either.</span></span> <span data-ttu-id="b1b94-122">Makinenizde Visual Studio zaten yüklüyse, sonraki iki adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-122">If you already have Visual Studio installed on your machine, skip the next two steps.</span></span>
   - <span data-ttu-id="b1b94-123">[Visual Studio 2017 yükleyicisi](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15)ni indirin.</span><span class="sxs-lookup"><span data-stu-id="b1b94-123">Download the [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="b1b94-124">Yükleyiciyi çalıştırın ve yükleme istemlerini izleyerek yüklemeyi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-124">Run the installer and follow the installation prompts to complete the installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="b1b94-125">**Visual Studio'yu yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="b1b94-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="b1b94-126">Visual Studio’dan, proje özelliği > yapılandırma özellikleri > C/C++ > bağlayıcı > genel > ek kitaplık dizinleri’ne gidip c++ bağlayıcısının lib\opt dizinini (ör. C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) ekleyin. </span><span class="sxs-lookup"><span data-stu-id="b1b94-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add the lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of the c++ connector.</span></span>
2. <span data-ttu-id="b1b94-127">Visual Studio'da proje özelliği > yapılandırma özellikleri > C/C++ > genel’e gidip ek dahil edilecek dizinler</span><span class="sxs-lookup"><span data-stu-id="b1b94-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="b1b94-128">c++ bağlayıcısının include/ dizin bilgisini ekleyin (ör. C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="b1b94-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="b1b94-129">Boost kitaplığının kök dizinini ekleyin (ör. C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="b1b94-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="b1b94-130">Visual Studio'dan proje özelliği > yapılandırma özellikleri > C/C++ > bağlayıcı > Giriş > Ek Bağımlılıklar’a gidip metin alanına mysqlcppconn.lib değerini ekleyin</span><span class="sxs-lookup"><span data-stu-id="b1b94-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into the text field</span></span>
4. <span data-ttu-id="b1b94-131">Adım 3'teki C ++ bağlayıcı kitaplık klasöründen mysqlcppconn.dll dosyasını uygulama yürütülebilir dosyasıyla aynı dizine kopyalayın ya da uygulamanızın dosyayı bulması için ortam değişkenine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b1b94-131">Either copy mysqlcppconn.dll from the c++ connector library folder in step 3 to the same directory as the application executable or add it to the environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="b1b94-132">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="b1b94-132">Get connection information</span></span>
<span data-ttu-id="b1b94-133">MySQL için Azure Veritabanı'na bağlanmak üzere gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="b1b94-134">Tam sunucu adına ve oturum açma kimlik bilgilerine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b1b94-135">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b1b94-136">Azure portalında sol taraftaki menüden **Tüm kaynaklar**'a tıklayın ve oluşturduğunuz sunucuyu (örneğin, **myserver4demo**) arayın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-136">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="b1b94-137">Sunucunun adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-137">Click the server name.</span></span>
4. <span data-ttu-id="b1b94-138">Sunucunun **Özellikler** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="b1b94-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="b1b94-139">**Sunucu adını** ve **Sunucu yöneticisi oturum açma adını** not edin.</span><span class="sxs-lookup"><span data-stu-id="b1b94-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b1b94-140">![MySQL için Azure Veritabanı sunucu adı](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="b1b94-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="b1b94-141">Sunucunuzun oturum açma bilgilerini unuttuysanız **Genel Bakış** sayfasına giderek Sunucu yöneticisi oturum açma adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="b1b94-142">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="b1b94-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="b1b94-143">Bağlanıp **CREATE TABLE** ve **INSERT INTO** SQL deyimlerini kullanarak verileri yüklemek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-143">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="b1b94-144">Kod MySQL ile bağlantı kurmak için connect() yöntemiyle sql::Driver sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-144">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b1b94-145">Ardından kod veritabanı komutlarını çalıştırmak için createStatement() ve execute() yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-145">Then the code uses method createStatement() and execute() to run the database commands.</span></span> 

<span data-ttu-id="b1b94-146">Host, DBName, User ve Password parametrelerini, sunucuyu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b1b94-146">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a><span data-ttu-id="b1b94-147">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="b1b94-147">Read data</span></span>

<span data-ttu-id="b1b94-148">Bağlanmak ve **SELECT** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-148">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="b1b94-149">Kod MySQL ile bağlantı kurmak için connect() yöntemiyle sql::Driver sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-149">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b1b94-150">Ardından kod, seçme komutlarını çalıştırmak için prepareStatement() ve executeQuery() yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-150">Then the code uses method prepareStatement() and executeQuery() to run the select commands.</span></span> <span data-ttu-id="b1b94-151">Son olarak kod next() yöntemini kullanarak sonuçlardaki kayıtlara gider.</span><span class="sxs-lookup"><span data-stu-id="b1b94-151">Finally the code uses next() to advance to the records in the results.</span></span> <span data-ttu-id="b1b94-152">Ardından kod getInt() ve getString() yöntemini kullanarak kayıttaki değerleri ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-152">Then the code uses getInt() and getString() to parse the values in the record.</span></span>

<span data-ttu-id="b1b94-153">Host, DBName, User ve Password parametrelerini, sunucuyu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b1b94-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="b1b94-154">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b1b94-154">Update data</span></span>
<span data-ttu-id="b1b94-155">Bağlanmak ve **UPDATE** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-155">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="b1b94-156">Kod MySQL ile bağlantı kurmak için connect() yöntemiyle sql::Driver sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-156">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b1b94-157">Ardından kod, güncelleme komutlarını çalıştırmak için prepareStatement() ve executeQuery() yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-157">Then the code uses method prepareStatement() and executeQuery() to run the update commands.</span></span> 

<span data-ttu-id="b1b94-158">Host, DBName, User ve Password parametrelerini, sunucuyu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b1b94-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="b1b94-159">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="b1b94-159">Delete data</span></span>
<span data-ttu-id="b1b94-160">Bağlanmak ve **DELETE** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1b94-160">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="b1b94-161">Kod MySQL ile bağlantı kurmak için connect() yöntemiyle sql::Driver sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-161">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="b1b94-162">Ardından kod, silme komutlarını çalıştırmak için prepareStatement() ve executeQuery() yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1b94-162">Then the code uses method prepareStatement() and executeQuery() to run the delete commands.</span></span>

<span data-ttu-id="b1b94-163">Host, DBName, User ve Password parametrelerini, sunucuyu ve veritabanını oluştururken belirttiğiniz değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b1b94-163">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="b1b94-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b1b94-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b1b94-165">Döküm alma ve geri yükleme işlemlerini kullanarak MySQL veritabanınızı MySQL için Azure Veritabanı'na geçirme</span><span class="sxs-lookup"><span data-stu-id="b1b94-165">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
