---
title: "C++ içinden MySQL için tooAzure veritabanına bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç MySQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz bir C++ kod örneğini sağlar."
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
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a><span data-ttu-id="d8d34-103">Azure veritabanı için MySQL: kullanım bağlayıcı/C++ tooconnect ve sorgu verileri</span><span class="sxs-lookup"><span data-stu-id="d8d34-103">Azure Database for MySQL: Use Connector/C++ tooconnect and query data</span></span>
<span data-ttu-id="d8d34-104">Bu hızlı başlangıç gösteren Azure tooconnect tooan veritabanı nasıl bir C++ uygulaması kullanarak MySQL için.</span><span class="sxs-lookup"><span data-stu-id="d8d34-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="d8d34-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="d8d34-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="d8d34-106">Merhaba bu makaledeki adımları C++ kullanarak geliştirme ile tanıdık olduğunuz ve Azure veritabanı için MySQL ile yeni tooworking olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d8d34-106">hello steps in this article assume that you are familiar with developing using C++, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8d34-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d8d34-107">Prerequisites</span></span>
<span data-ttu-id="d8d34-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="d8d34-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="d8d34-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d8d34-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="d8d34-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d8d34-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="d8d34-111">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d8d34-111">You also need to:</span></span>
- <span data-ttu-id="d8d34-112">[.Net Framework](https://www.microsoft.com/net/download)'ü yükleme</span><span class="sxs-lookup"><span data-stu-id="d8d34-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="d8d34-113">[Visual Studio](https://www.visualstudio.com/downloads/)'yu yükleme</span><span class="sxs-lookup"><span data-stu-id="d8d34-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="d8d34-114">[MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/) yükleyin</span><span class="sxs-lookup"><span data-stu-id="d8d34-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="d8d34-115">[Boost](http://www.boost.org/)’u yükleyin</span><span class="sxs-lookup"><span data-stu-id="d8d34-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="d8d34-116">Visual Studio'yu ve .NET'i yükleme</span><span class="sxs-lookup"><span data-stu-id="d8d34-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="d8d34-117">Bu bölümdeki Hello adımları geliştirme .NET kullanma hakkında bilgi sahibi olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d8d34-117">hello steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="d8d34-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="d8d34-118">**Windows**</span></span>
1. <span data-ttu-id="d8d34-119">Android, iOS ve Windows’un yanı sıra web ve veritabanı uygulamaları ile bulut hizmetleri için modern uygulamalar oluşturmaya yönelik tam özellikli, genişletilebilir, ücretsiz bir IDE olan Visual Studio 2017 Community’yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d8d34-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="d8d34-120">Merhaba tam .NET Framework veya .NET Core yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8d34-120">You can install either hello full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="d8d34-121">kod parçacıkları hello hızlı başlangıç çalışma ya da ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="d8d34-121">hello code snippets in hello Quickstart work with either.</span></span> <span data-ttu-id="d8d34-122">Visual Studio yüklüyse, makinenizde zaten varsa, hello sonraki iki adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="d8d34-122">If you already have Visual Studio installed on your machine, skip hello next two steps.</span></span>
   - <span data-ttu-id="d8d34-123">Merhaba karşıdan [Visual Studio 2017 yükleyici](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="d8d34-123">Download hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="d8d34-124">Merhaba yükleyiciyi çalıştırın ve hello yükleme istemleri toocomplete hello yükleme izleyin.</span><span class="sxs-lookup"><span data-stu-id="d8d34-124">Run hello installer and follow hello installation prompts toocomplete hello installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="d8d34-125">**Visual Studio'yu yapılandırma**</span><span class="sxs-lookup"><span data-stu-id="d8d34-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="d8d34-126">Visual Studio'dan özellik Proje > yapılandırma özellikleri > C/C++ > bağlayıcı > Genel > ek kitaplık dizinleri hello lib\opt dizin ekleyin (ör: C:\Program Files (x86) \MySQL\MySQL bağlayıcı C++ 1.1.9\lib\opt), hello c ++ Bağlayıcı.</span><span class="sxs-lookup"><span data-stu-id="d8d34-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add hello lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of hello c++ connector.</span></span>
2. <span data-ttu-id="d8d34-127">Visual Studio'da proje özelliği > yapılandırma özellikleri > C/C++ > genel’e gidip ek dahil edilecek dizinler</span><span class="sxs-lookup"><span data-stu-id="d8d34-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="d8d34-128">c++ bağlayıcısının include/ dizin bilgisini ekleyin (ör. C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="d8d34-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="d8d34-129">Boost kitaplığının kök dizinini ekleyin (ör. C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="d8d34-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="d8d34-130">Visual Studio'dan özellik Proje > yapılandırma özellikleri > C/C++ > bağlayıcı > giriş > ek bağımlılıklar mysqlcppconn.lib hello metin alanına ekleyin</span><span class="sxs-lookup"><span data-stu-id="d8d34-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into hello text field</span></span>
4. <span data-ttu-id="d8d34-131">Her iki kopya mysqlcppconn.dll hello c ++ Bağlayıcısı Kitaplığı'ndaki klasöründen 3. adım toohello yürütülebilir Merhaba uygulaması ile aynı dizinde veya uygulamanızın bulabilmesi toohello ortam değişkeni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d8d34-131">Either copy mysqlcppconn.dll from hello c++ connector library folder in step 3 toohello same directory as hello application executable or add it toohello environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="d8d34-132">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="d8d34-132">Get connection information</span></span>
<span data-ttu-id="d8d34-133">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın.</span><span class="sxs-lookup"><span data-stu-id="d8d34-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="d8d34-134">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8d34-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="d8d34-135">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d8d34-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d8d34-136">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="d8d34-136">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="d8d34-137">Merhaba sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8d34-137">Click hello server name.</span></span>
4. <span data-ttu-id="d8d34-138">Select hello sunucunun **özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="d8d34-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="d8d34-139">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="d8d34-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="d8d34-140">![MySQL için Azure Veritabanı sunucu adı](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="d8d34-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="d8d34-141">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="d8d34-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="d8d34-142">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="d8d34-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="d8d34-143">Kullanım hello aşağıdakileri tooconnect kod ve verileri hello kullanarak yük **CREATE TABLE** ve **INSERT INTO** SQL deyimlerini.</span><span class="sxs-lookup"><span data-stu-id="d8d34-143">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="d8d34-144">Merhaba kod hello connect() yöntemi tooestablish bağlantı tooMySQL sql::Driver sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8d34-144">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="d8d34-145">Daha sonra hello kod yöntemi createStatement() ve execute() toorun hello veritabanı komutlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8d34-145">Then hello code uses method createStatement() and execute() toorun hello database commands.</span></span> 

<span data-ttu-id="d8d34-146">Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d8d34-146">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="read-data"></a><span data-ttu-id="d8d34-147">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="d8d34-147">Read data</span></span>

<span data-ttu-id="d8d34-148">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="d8d34-148">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="d8d34-149">Merhaba kod hello connect() yöntemi tooestablish bağlantı tooMySQL sql::Driver sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8d34-149">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="d8d34-150">Ardından hello kod yöntemi prepareStatement() kullanır ve executeQuery() toorun hello komutları seçin.</span><span class="sxs-lookup"><span data-stu-id="d8d34-150">Then hello code uses method prepareStatement() and executeQuery() toorun hello select commands.</span></span> <span data-ttu-id="d8d34-151">Son olarak hello kodu next() tooadvance toohello kayıtları hello sonuçlarında kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8d34-151">Finally hello code uses next() tooadvance toohello records in hello results.</span></span> <span data-ttu-id="d8d34-152">Daha sonra hello kod hello kaydında getInt() ve getString() tooparse hello değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8d34-152">Then hello code uses getInt() and getString() tooparse hello values in hello record.</span></span>

<span data-ttu-id="d8d34-153">Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d8d34-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="update-data"></a><span data-ttu-id="d8d34-154">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d8d34-154">Update data</span></span>
<span data-ttu-id="d8d34-155">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="d8d34-155">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="d8d34-156">Merhaba kod hello connect() yöntemi tooestablish bağlantı tooMySQL sql::Driver sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8d34-156">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="d8d34-157">Daha sonra hello kod yöntemi prepareStatement() ve executeQuery() toorun hello güncelleştirme komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8d34-157">Then hello code uses method prepareStatement() and executeQuery() toorun hello update commands.</span></span> 

<span data-ttu-id="d8d34-158">Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d8d34-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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


## <a name="delete-data"></a><span data-ttu-id="d8d34-159">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="d8d34-159">Delete data</span></span>
<span data-ttu-id="d8d34-160">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="d8d34-160">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="d8d34-161">Merhaba kod hello connect() yöntemi tooestablish bağlantı tooMySQL sql::Driver sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8d34-161">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="d8d34-162">Daha sonra hello kod yöntemi prepareStatement() kullanır ve executeQuery() toorun hello komutları silin.</span><span class="sxs-lookup"><span data-stu-id="d8d34-162">Then hello code uses method prepareStatement() and executeQuery() toorun hello delete commands.</span></span>

<span data-ttu-id="d8d34-163">Merhaba konak, DBName, kullanıcı ve parola parametrelerini hello sunucu ve veritabanı oluşturduğunuzda belirttiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d8d34-163">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="next-steps"></a><span data-ttu-id="d8d34-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d8d34-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d8d34-165">MySQL veritabanı tooAzure veritabanı için MySQL döküm ve geri yükleme kullanarak geçirme</span><span class="sxs-lookup"><span data-stu-id="d8d34-165">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
