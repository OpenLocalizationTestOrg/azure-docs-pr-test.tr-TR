---
title: "TooAzure veritabanı için MySQL Git kullanarak bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıç MySQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz birkaç Git kod örnekleri sağlar."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: e8067b807ee729e04850c5325f476806bcd54983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="809c5-103">Azure veritabanı için MySQL: dil tooconnect ve sorgu veri kullanımı gidin</span><span class="sxs-lookup"><span data-stu-id="809c5-103">Azure Database for MySQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="809c5-104">Bu hızlı başlangıç gösterir nasıl MySQL kullanma tooconnect tooan Azure veritabanı kod yazılmış Merhaba [Git](https://golang.org/) macOS platformları Windows, Ubuntu Linux ve Apple dili.</span><span class="sxs-lookup"><span data-stu-id="809c5-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using code written in hello [Go](https://golang.org/) language from Windows, Ubuntu Linux, and Apple macOS platforms.</span></span> <span data-ttu-id="809c5-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="809c5-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="809c5-106">Bu makale, Azure veritabanı için MySQL ile yeni tooworking olan ancak bu, Git, kullanarak geliştirme ile bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="809c5-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="809c5-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="809c5-107">Prerequisites</span></span>
<span data-ttu-id="809c5-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="809c5-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="809c5-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="809c5-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="809c5-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="809c5-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="809c5-111">Go ve MySQL bağlayıcısını yükleme</span><span class="sxs-lookup"><span data-stu-id="809c5-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="809c5-112">Yükleme [Git](https://golang.org/doc/install) ve hello [MySQL için Git-sql-sürücü](https://github.com/go-sql-driver/mysql#installation) kendi makinede.</span><span class="sxs-lookup"><span data-stu-id="809c5-112">Install [Go](https://golang.org/doc/install) and hello [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own machine.</span></span> <span data-ttu-id="809c5-113">Platformunuz bağlı olarak hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="809c5-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="809c5-114">Windows</span><span class="sxs-lookup"><span data-stu-id="809c5-114">Windows</span></span>
1. <span data-ttu-id="809c5-115">[Karşıdan](https://golang.org/dl/) ve Microsoft toohello göre Windows için Git yükleme [yükleme yönergeleri](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="809c5-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="809c5-116">Merhaba Başlat menüsünden Hello komut istemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="809c5-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="809c5-117">Projeniz için şöyle bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="809c5-117">Make a folder for your project such.</span></span> <span data-ttu-id="809c5-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="809c5-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="809c5-119">Dizin hello proje klasörüne gibi değiştirmek `cd %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="809c5-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="809c5-120">Merhaba ortam değişkeni GOPATH toopoint toohello kaynak kod dizini için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="809c5-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="809c5-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="809c5-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="809c5-122">Merhaba yüklemek [mysql için Git-sql-sürücü](https://github.com/go-sql-driver/mysql#installation) hello çalıştırarak `go get github.com/go-sql-driver/mysql` komutu.</span><span class="sxs-lookup"><span data-stu-id="809c5-122">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="809c5-123">Özet olarak, Git yüklemeniz ve ardından hello komut isteminde şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="809c5-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="809c5-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="809c5-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="809c5-125">Merhaba Bash kabuğunda başlatın.</span><span class="sxs-lookup"><span data-stu-id="809c5-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="809c5-126">`sudo apt-get install golang-go` komutunu çalıştırarak Go'yu yükleyin.</span><span class="sxs-lookup"><span data-stu-id="809c5-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="809c5-127">Giriş dizininizde projeniz için `mkdir -p ~/go/src/mysqlgo/` gibi bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="809c5-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="809c5-128">Dizin hello klasörüne gibi değiştirmek `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="809c5-128">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="809c5-129">Kümesi hello GOPATH ortam değişkeni toopoint tooa geçerli bir kaynak dizini, geçerli ev gibi dizinin klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="809c5-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="809c5-130">Merhaba bash kabuğunda çalıştırmak `export GOPATH=~/go` tooadd hello hello geçerli kabuk oturumu için GOPATH hello gibi dizin gidin.</span><span class="sxs-lookup"><span data-stu-id="809c5-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="809c5-131">Merhaba yüklemek [mysql için Git-sql-sürücü](https://github.com/go-sql-driver/mysql#installation) hello çalıştırarak `go get github.com/go-sql-driver/mysql` komutu.</span><span class="sxs-lookup"><span data-stu-id="809c5-131">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="809c5-132">Özetle, şu bash komutlarını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="809c5-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="809c5-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="809c5-133">Apple macOS</span></span>
1. <span data-ttu-id="809c5-134">İndirme ve yükleme toohello göre Git [yükleme yönergeleri](https://golang.org/doc/install) platformunuz eşleşen.</span><span class="sxs-lookup"><span data-stu-id="809c5-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="809c5-135">Merhaba Bash kabuğunda başlatın.</span><span class="sxs-lookup"><span data-stu-id="809c5-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="809c5-136">Giriş dizininizde projeniz için `mkdir -p ~/go/src/mysqlgo/` gibi bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="809c5-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="809c5-137">Dizin hello klasörüne gibi değiştirmek `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="809c5-137">Change directory into hello folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="809c5-138">Kümesi hello GOPATH ortam değişkeni toopoint tooa geçerli bir kaynak dizini, geçerli ev gibi dizinin klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="809c5-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="809c5-139">Merhaba bash kabuğunda çalıştırmak `export GOPATH=~/go` tooadd hello hello geçerli kabuk oturumu için GOPATH hello gibi dizin gidin.</span><span class="sxs-lookup"><span data-stu-id="809c5-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="809c5-140">Merhaba yüklemek [mysql için Git-sql-sürücü](https://github.com/go-sql-driver/mysql#installation) hello çalıştırarak `go get github.com/go-sql-driver/mysql` komutu.</span><span class="sxs-lookup"><span data-stu-id="809c5-140">Install hello [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running hello `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="809c5-141">Özetle, Go’yu yükleyin ve ardından şu bash komutlarını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="809c5-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="809c5-142">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="809c5-142">Get connection information</span></span>
<span data-ttu-id="809c5-143">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için MySQL alın.</span><span class="sxs-lookup"><span data-stu-id="809c5-143">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="809c5-144">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="809c5-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="809c5-145">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="809c5-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="809c5-146">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve aramak için creased, gibi hello sunucu **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="809c5-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="809c5-147">Merhaba sunucu adına tıklatarak **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="809c5-147">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="809c5-148">Select hello sunucunun **özellikleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="809c5-148">Select hello server's **Properties** page.</span></span> <span data-ttu-id="809c5-149">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="809c5-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="809c5-150">![MySQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma](./media/connect-go/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="809c5-150">![Azure Database for MySQL - Server Admin Login](./media/connect-go/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="809c5-151">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** tooview hello sunucu yönetici oturum açma adı sayfasında ve gerekirse sıfırlamak hello parola.</span><span class="sxs-lookup"><span data-stu-id="809c5-151">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="809c5-152">Go kodunu derleme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="809c5-152">Build and run Go code</span></span> 
1. <span data-ttu-id="809c5-153">toowrite Golang kodu, Microsoft Windows, Not Defteri gibi bir basit bir metin düzenleyicisi kullanabilirsiniz [VI](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) veya [Nano](https://www.nano-editor.org/) Ubuntu ya da macOS TextEdit.</span><span class="sxs-lookup"><span data-stu-id="809c5-153">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="809c5-154">Daha zengin bir Tümleşik Geliştirme Ortamı (IDE) tercih ediyorsanız [Atom](https://atom.io/), Jetbrains [Gogland](https://www.jetbrains.com/go/) veya Microsoft [Visual Studio Code](https://code.visualstudio.com/) kullanmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="809c5-154">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="809c5-155">Merhaba hello bölümlere Git koddan metin dosyasına yapıştırın ve proje klasörünüzdeki dosya uzantısına sahip saklamalısınız \*Windows yolu gibi .go `%USERPROFILE%\go\src\mysqlgo\createtable.go` ya da Linux yolu `~/go/src/mysqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="809c5-155">Paste hello Go code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="809c5-156">Merhaba bulun `HOST`, `DATABASE`, `USER`, ve `PASSWORD` sabitleri hello kod ve kendi değerlerle değiştirin hello örnek değerler.</span><span class="sxs-lookup"><span data-stu-id="809c5-156">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span> 
4. <span data-ttu-id="809c5-157">Merhaba komut istemi başlatın veya kabuk bash.</span><span class="sxs-lookup"><span data-stu-id="809c5-157">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="809c5-158">Dizini değiştirerek proje klasörünüze geçin.</span><span class="sxs-lookup"><span data-stu-id="809c5-158">Change directory into your project folder.</span></span> <span data-ttu-id="809c5-159">Örneğin; Windows’da `cd %USERPROFILE%\go\src\mysqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="809c5-159">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="809c5-160">Linux'ta `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="809c5-160">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="809c5-161">Belirtilen hello IDE düzenleyicileri bazıları, hata ayıklama ve çalışma zamanı yeteneklerini Kabuk komutları gerek kalmadan sunar.</span><span class="sxs-lookup"><span data-stu-id="809c5-161">Some of hello IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="809c5-162">Merhaba komutu yazarak Hello kodu çalıştırma `go run createtable.go` toocompile hello uygulama ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="809c5-162">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="809c5-163">Alternatif olarak, toobuild hello kodu yerel bir uygulamaya `go build createtable.go`, ardından başlatma `createtable.exe` toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="809c5-163">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="809c5-164">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="809c5-164">Connect, create table, and insert data</span></span>
<span data-ttu-id="809c5-165">Kullanım hello aşağıdaki kod tooconnect toohello sunucu, bir tablo oluşturun ve verileri hello kullanarak yük bir **Ekle** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="809c5-165">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="809c5-166">Merhaba kod üç paketlerini içeri aktarır: hello [sql paketi](https://golang.org/pkg/database/sql/), hello [gidin sql sürücüsü mysql için](https://github.com/go-sql-driver/mysql#installation) sürücü toocommunicate hello Azure veritabanı için MySQL ve hello olarak [fmt paket](https://golang.org/pkg/fmt/)yazdırılan giriş ve çıkış hello komut satırında için.</span><span class="sxs-lookup"><span data-stu-id="809c5-166">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="809c5-167">Merhaba kod yöntemi çağırır [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure veritabanı için MySQL ve denetimleri hello bağlantı yöntemini kullanarak [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="809c5-167">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="809c5-168">A [veritabanı işleci](https://golang.org/pkg/database/sql/#DB) boyunca, hello bağlantı havuzu hello veritabanı sunucusu için bulunduran kullanılır.</span><span class="sxs-lookup"><span data-stu-id="809c5-168">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="809c5-169">Merhaba kod çağrıları hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) yöntemi birkaç kez toorun birkaç DDL komutları.</span><span class="sxs-lookup"><span data-stu-id="809c5-169">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several DDL commands.</span></span> <span data-ttu-id="809c5-170">Merhaba kodu da hello kullanan [Prepare()](http://go-database-sql.org/prepared.html) ve Exec() toorun hazırlanan farklı parametrelerle deyimleri tooinsert üç satır.</span><span class="sxs-lookup"><span data-stu-id="809c5-170">hello code also uses hello [Prepare()](http://go-database-sql.org/prepared.html) and Exec() toorun prepared statements with different parameters tooinsert three rows.</span></span> <span data-ttu-id="809c5-171">Bir hata oluştu ve tooexit Panik her zaman bir özel checkError() kullanılan toocheck yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="809c5-171">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="809c5-172">Hello yerine `host`, `database`, `user`, ve `password` sabitleri kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="809c5-172">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a><span data-ttu-id="809c5-173">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="809c5-173">Read data</span></span>
<span data-ttu-id="809c5-174">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="809c5-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="809c5-175">Merhaba kod üç paketlerini içeri aktarır: hello [sql paketi](https://golang.org/pkg/database/sql/), hello [gidin sql sürücüsü mysql için](https://github.com/go-sql-driver/mysql#installation) sürücü toocommunicate hello Azure veritabanı için MySQL ve hello olarak [fmt paket](https://golang.org/pkg/fmt/)yazdırılan giriş ve çıkış hello komut satırında için.</span><span class="sxs-lookup"><span data-stu-id="809c5-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="809c5-176">Merhaba kod yöntemi çağırır [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure veritabanı için MySQL ve denetimleri hello bağlantı yöntemini kullanarak [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="809c5-176">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="809c5-177">A [veritabanı işleci](https://golang.org/pkg/database/sql/#DB) boyunca, hello bağlantı havuzu hello veritabanı sunucusu için bulunduran kullanılır.</span><span class="sxs-lookup"><span data-stu-id="809c5-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="809c5-178">Merhaba kod çağrıları hello [Query()](https://golang.org/pkg/database/sql/#DB.Query) yöntemi toorun hello select komutu.</span><span class="sxs-lookup"><span data-stu-id="809c5-178">hello code calls hello [Query()](https://golang.org/pkg/database/sql/#DB.Query) method toorun hello select command.</span></span> <span data-ttu-id="809c5-179">Çalıştıktan sonra [Next()](https://golang.org/pkg/database/sql/#Rows.Next) hello sonuç kümesi aracılığıyla tooiterate ve [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello sütun değerleri, değişkenlere hello değeri kaydetme.</span><span class="sxs-lookup"><span data-stu-id="809c5-179">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate through hello result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello column values, saving hello value into variables.</span></span> <span data-ttu-id="809c5-180">Bir hata oluştu ve tooexit Panik her zaman bir özel checkError() kullanılan toocheck yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="809c5-180">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="809c5-181">Hello yerine `host`, `database`, `user`, ve `password` sabitleri kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="809c5-181">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from hello table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a><span data-ttu-id="809c5-182">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="809c5-182">Update data</span></span>
<span data-ttu-id="809c5-183">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="809c5-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="809c5-184">Merhaba kod üç paketlerini içeri aktarır: hello [sql paketi](https://golang.org/pkg/database/sql/), hello [gidin sql sürücüsü mysql için](https://github.com/go-sql-driver/mysql#installation) sürücü toocommunicate hello Azure veritabanı için MySQL ve hello olarak [fmt paket](https://golang.org/pkg/fmt/)yazdırılan giriş ve çıkış hello komut satırında için.</span><span class="sxs-lookup"><span data-stu-id="809c5-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="809c5-185">Merhaba kod yöntemi çağırır [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure veritabanı için MySQL ve denetimleri hello bağlantı yöntemini kullanarak [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="809c5-185">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="809c5-186">A [veritabanı işleci](https://golang.org/pkg/database/sql/#DB) boyunca, hello bağlantı havuzu hello veritabanı sunucusu için bulunduran kullanılır.</span><span class="sxs-lookup"><span data-stu-id="809c5-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="809c5-187">Merhaba kod çağrıları hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) yöntemi toorun hello güncelleştirme komutu.</span><span class="sxs-lookup"><span data-stu-id="809c5-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello update command.</span></span> <span data-ttu-id="809c5-188">Bir hata oluştu ve tooexit Panik her zaman bir özel checkError() kullanılan toocheck yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="809c5-188">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="809c5-189">Hello yerine `host`, `database`, `user`, ve `password` sabitleri kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="809c5-189">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a><span data-ttu-id="809c5-190">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="809c5-190">Delete data</span></span>
<span data-ttu-id="809c5-191">Kullanım hello aşağıdaki tooconnect kod ve verileri kullanarak kaldırma bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="809c5-191">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="809c5-192">Merhaba kod üç paketlerini içeri aktarır: hello [sql paketi](https://golang.org/pkg/database/sql/), hello [gidin sql sürücüsü mysql için](https://github.com/go-sql-driver/mysql#installation) sürücü toocommunicate hello Azure veritabanı için MySQL ve hello olarak [fmt paket](https://golang.org/pkg/fmt/)yazdırılan giriş ve çıkış hello komut satırında için.</span><span class="sxs-lookup"><span data-stu-id="809c5-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver toocommunicate with hello Azure Database for MySQL, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="809c5-193">Merhaba kod yöntemi çağırır [sql. Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure veritabanı için MySQL ve denetimleri hello bağlantı yöntemini kullanarak [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="809c5-193">hello code calls method [sql.Open()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database for MySQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="809c5-194">A [veritabanı işleci](https://golang.org/pkg/database/sql/#DB) boyunca, hello bağlantı havuzu hello veritabanı sunucusu için bulunduran kullanılır.</span><span class="sxs-lookup"><span data-stu-id="809c5-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="809c5-195">Merhaba kod çağrıları hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) yöntemi toorun hello Sil komutu.</span><span class="sxs-lookup"><span data-stu-id="809c5-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello delete command.</span></span> <span data-ttu-id="809c5-196">Bir hata oluştu ve tooexit Panik her zaman bir özel checkError() kullanılan toocheck yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="809c5-196">Each time a custom checkError() method is used toocheck if an error occurred and panic tooexit.</span></span>

<span data-ttu-id="809c5-197">Hello yerine `host`, `database`, `user`, ve `password` sabitleri kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="809c5-197">Replace hello `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a><span data-ttu-id="809c5-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="809c5-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="809c5-199">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="809c5-199">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
