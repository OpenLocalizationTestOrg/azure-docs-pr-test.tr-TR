---
title: "aaaConnect tooAzure Git dilini kullanarak PostgreSQL için veritabanı | Microsoft Docs"
description: "Bu hızlı başlangıç PostgreSQL için Azure veritabanındaki verileri sorgulamak ve tooconnect için kullanabileceğiniz bir Git programlama dili örneğini sağlar."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="14ad9-103">Azure veritabanı PostgreSQL için: dil tooconnect ve sorgu veri kullanımı gidin</span><span class="sxs-lookup"><span data-stu-id="14ad9-103">Azure Database for PostgreSQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="14ad9-104">Bu hızlı başlangıç gösteren nasıl PostgreSQL kullanma tooconnect tooan Azure veritabanı kod yazılmış Merhaba [Git](https://golang.org/) dili (golang).</span><span class="sxs-lookup"><span data-stu-id="14ad9-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using code written in hello [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="14ad9-105">Nasıl toouse SQL deyimleri tooquery, Ekle, Güncelleştir ve hello veritabanında bulunan verileri silme gösterir.</span><span class="sxs-lookup"><span data-stu-id="14ad9-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="14ad9-106">Bu makale, yeni tooworking PostgreSQL için Azure veritabanıyla olan ancak bu, Git, kullanarak geliştirme ile bildiğinizi varsayar.</span><span class="sxs-lookup"><span data-stu-id="14ad9-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14ad9-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="14ad9-107">Prerequisites</span></span>
<span data-ttu-id="14ad9-108">Bu hızlı başlangıç Bu kılavuzlara birini başlangıç noktası olarak oluşturulan hello kaynakları kullanır:</span><span class="sxs-lookup"><span data-stu-id="14ad9-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="14ad9-109">DB Oluşturma - Portal</span><span class="sxs-lookup"><span data-stu-id="14ad9-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="14ad9-110">DB Oluşturma - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="14ad9-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="14ad9-111">Go ve pq bağlayıcısını yükleme</span><span class="sxs-lookup"><span data-stu-id="14ad9-111">Install Go and pq connector</span></span>
<span data-ttu-id="14ad9-112">Yükleme [Git](https://golang.org/doc/install) ve hello [saf Git Postgres sürücüsü (pq)](https://github.com/lib/pq) kendi makinede.</span><span class="sxs-lookup"><span data-stu-id="14ad9-112">Install [Go](https://golang.org/doc/install) and hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="14ad9-113">Platformunuz bağlı olarak hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="14ad9-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="14ad9-114">Windows</span><span class="sxs-lookup"><span data-stu-id="14ad9-114">Windows</span></span>
1. <span data-ttu-id="14ad9-115">[Karşıdan](https://golang.org/dl/) ve Microsoft toohello göre Windows için Git yükleme [yükleme yönergeleri](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="14ad9-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="14ad9-116">Merhaba Başlat menüsünden Hello komut istemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="14ad9-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="14ad9-117">Projeniz için şöyle bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="14ad9-117">Make a folder for your project such.</span></span> <span data-ttu-id="14ad9-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="14ad9-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="14ad9-119">Dizin hello proje klasörüne gibi değiştirmek `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="14ad9-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="14ad9-120">Merhaba ortam değişkeni GOPATH toopoint toohello kaynak kod dizini için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="14ad9-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="14ad9-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="14ad9-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="14ad9-122">Merhaba yüklemek [saf Git Postgres sürücüsü (pq)](https://github.com/lib/pq) hello çalıştırarak `go get github.com/lib/pq` komutu.</span><span class="sxs-lookup"><span data-stu-id="14ad9-122">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="14ad9-123">Özet olarak, Git yüklemeniz ve ardından hello komut isteminde şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="14ad9-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="14ad9-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="14ad9-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="14ad9-125">Merhaba Bash kabuğunda başlatın.</span><span class="sxs-lookup"><span data-stu-id="14ad9-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="14ad9-126">`sudo apt-get install golang-go` komutunu çalıştırarak Go'yu yükleyin.</span><span class="sxs-lookup"><span data-stu-id="14ad9-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="14ad9-127">Giriş dizininizde projeniz için `mkdir -p ~/go/src/postgresqlgo/` gibi bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="14ad9-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="14ad9-128">Dizin hello klasörüne gibi değiştirmek `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="14ad9-128">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="14ad9-129">Kümesi hello GOPATH ortam değişkeni toopoint tooa geçerli bir kaynak dizini, geçerli ev gibi dizinin klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="14ad9-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="14ad9-130">Merhaba bash kabuğunda çalıştırmak `export GOPATH=~/go` tooadd hello hello geçerli kabuk oturumu için GOPATH hello gibi dizin gidin.</span><span class="sxs-lookup"><span data-stu-id="14ad9-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="14ad9-131">Merhaba yüklemek [saf Git Postgres sürücüsü (pq)](https://github.com/lib/pq) hello çalıştırarak `go get github.com/lib/pq` komutu.</span><span class="sxs-lookup"><span data-stu-id="14ad9-131">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="14ad9-132">Özetle, şu bash komutlarını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="14ad9-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="14ad9-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="14ad9-133">Apple macOS</span></span>
1. <span data-ttu-id="14ad9-134">İndirme ve yükleme toohello göre Git [yükleme yönergeleri](https://golang.org/doc/install) platformunuz eşleşen.</span><span class="sxs-lookup"><span data-stu-id="14ad9-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="14ad9-135">Merhaba Bash kabuğunda başlatın.</span><span class="sxs-lookup"><span data-stu-id="14ad9-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="14ad9-136">Giriş dizininizde projeniz için `mkdir -p ~/go/src/postgresqlgo/` gibi bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="14ad9-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="14ad9-137">Dizin hello klasörüne gibi değiştirmek `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="14ad9-137">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="14ad9-138">Kümesi hello GOPATH ortam değişkeni toopoint tooa geçerli bir kaynak dizini, geçerli ev gibi dizinin klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="14ad9-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="14ad9-139">Merhaba bash kabuğunda çalıştırmak `export GOPATH=~/go` tooadd hello hello geçerli kabuk oturumu için GOPATH hello gibi dizin gidin.</span><span class="sxs-lookup"><span data-stu-id="14ad9-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="14ad9-140">Merhaba yüklemek [saf Git Postgres sürücüsü (pq)](https://github.com/lib/pq) hello çalıştırarak `go get github.com/lib/pq` komutu.</span><span class="sxs-lookup"><span data-stu-id="14ad9-140">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="14ad9-141">Özetle, Go’yu yükleyin ve ardından şu bash komutlarını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="14ad9-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="14ad9-142">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="14ad9-142">Get connection information</span></span>
<span data-ttu-id="14ad9-143">Merhaba bağlantı gerekli bilgileri tooconnect toohello Azure veritabanı için PostgreSQL alın.</span><span class="sxs-lookup"><span data-stu-id="14ad9-143">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="14ad9-144">Tam sunucu adını ve oturum açma kimlik bilgileri hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="14ad9-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="14ad9-145">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="14ad9-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="14ad9-146">Merhaba sol taraftaki menüden Azure portalında, **tüm kaynakları** ve oluşturduğunuz, gibi hello sunucu araması **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="14ad9-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="14ad9-147">Merhaba sunucu adına tıklatarak **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="14ad9-147">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="14ad9-148">Select hello sunucunun **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="14ad9-148">Select hello server's **Overview** page.</span></span> <span data-ttu-id="14ad9-149">Merhaba Not **sunucu adı** ve **sunucu yönetici oturum açma adı**.</span><span class="sxs-lookup"><span data-stu-id="14ad9-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="14ad9-150">![PostgreSQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma Bilgileri](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="14ad9-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="14ad9-151">Sunucu oturum açma bilgilerinizi unutursanız, toohello gidin **genel bakış** sayfası ve görünüm hello sunucu yönetici oturum açma adı.</span><span class="sxs-lookup"><span data-stu-id="14ad9-151">If you forget your server login information, navigate toohello **Overview** page, and view hello Server admin login name.</span></span> <span data-ttu-id="14ad9-152">Gerekirse, hello parola sıfırlama.</span><span class="sxs-lookup"><span data-stu-id="14ad9-152">If necessary, reset hello password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="14ad9-153">Go kodunu derleme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="14ad9-153">Build and run Go code</span></span> 
1. <span data-ttu-id="14ad9-154">toowrite Golang kodu, Microsoft Windows, Not Defteri gibi bir basit bir metin düzenleyicisi kullanabilirsiniz [VI](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) veya [Nano](https://www.nano-editor.org/) Ubuntu ya da macOS TextEdit.</span><span class="sxs-lookup"><span data-stu-id="14ad9-154">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="14ad9-155">Daha zengin bir Tümleşik Geliştirme Ortamı (IDE) tercih ediyorsanız [Atom](https://atom.io/), Jetbrains [Gogland](https://www.jetbrains.com/go/) veya Microsoft [Visual Studio Code](https://code.visualstudio.com/) kullanmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14ad9-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="14ad9-156">Merhaba Golang kodu hello bölümlerden metin dosyasına yapıştırın ve proje klasörünüzdeki dosya uzantısına sahip saklamalısınız \*Windows yolu gibi .go `%USERPROFILE%\go\src\postgresqlgo\createtable.go` ya da Linux yolu `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="14ad9-156">Paste hello Golang code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="14ad9-157">Merhaba bulun `HOST`, `DATABASE`, `USER`, ve `PASSWORD` sabitleri hello kod ve kendi değerlerle değiştirin hello örnek değerler.</span><span class="sxs-lookup"><span data-stu-id="14ad9-157">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span>  
4. <span data-ttu-id="14ad9-158">Merhaba komut istemi başlatın veya kabuk bash.</span><span class="sxs-lookup"><span data-stu-id="14ad9-158">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="14ad9-159">Dizini değiştirerek proje klasörünüze geçin.</span><span class="sxs-lookup"><span data-stu-id="14ad9-159">Change directory into your project folder.</span></span> <span data-ttu-id="14ad9-160">Örneğin; Windows’da `cd %USERPROFILE%\go\src\postgresqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="14ad9-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="14ad9-161">Linux'ta `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="14ad9-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="14ad9-162">Belirtilen hello IDE ortamları bazıları, hata ayıklama ve çalışma zamanı yeteneklerini Kabuk komutları gerek kalmadan sunar.</span><span class="sxs-lookup"><span data-stu-id="14ad9-162">Some of hello IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="14ad9-163">Merhaba komutu yazarak Hello kodu çalıştırma `go run createtable.go` toocompile hello uygulama ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="14ad9-163">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="14ad9-164">Alternatif olarak, toobuild hello kodu yerel bir uygulamaya `go build createtable.go`, ardından başlatma `createtable.exe` toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="14ad9-164">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="14ad9-165">Bağlanma ve tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="14ad9-165">Connect and create a table</span></span>
<span data-ttu-id="14ad9-166">Kullanım hello aşağıdakileri tooconnect kod ve kullanarak bir tablo oluşturmak **CREATE TABLE** SQL deyimi, arkasından **INSERT INTO** SQL deyimleri tooadd satırları hello tabloya.</span><span class="sxs-lookup"><span data-stu-id="14ad9-166">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="14ad9-167">Merhaba kod üç paketlerini içeri aktarır: Merhaba [sql paketi](https://golang.org/pkg/database/sql/), hello [pq paket](http://godoc.org/github.com/lib/pq) sürücü toocommunicate hello Postgres sunucu ve hello olarak [fmt paket](https://golang.org/pkg/fmt/) yazdırılması için Giriş ve çıkış hello komut satırında.</span><span class="sxs-lookup"><span data-stu-id="14ad9-167">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="14ad9-168">Merhaba kod yöntemi çağırır [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL ve denetimleri hello bağlantı yöntemini kullanarak veritabanı [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="14ad9-168">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="14ad9-169">A [veritabanı işleci](https://golang.org/pkg/database/sql/#DB) boyunca, hello bağlantı havuzu hello veritabanı sunucusu için bulunduran kullanılır.</span><span class="sxs-lookup"><span data-stu-id="14ad9-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="14ad9-170">Merhaba kod çağrıları hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) yöntemi birkaç kez toorun birkaç SQL komutları.</span><span class="sxs-lookup"><span data-stu-id="14ad9-170">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several SQL commands.</span></span> <span data-ttu-id="14ad9-171">Her bir hata oluştu, özel checkError() yöntemi toocheck ve zaman bir hata oluşursa tooexit Panik.</span><span class="sxs-lookup"><span data-stu-id="14ad9-171">Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="14ad9-172">Hello yerine `HOST`, `DATABASE`, `USER`, ve `PASSWORD` kendi değerlerinizi parametrelerle.</span><span class="sxs-lookup"><span data-stu-id="14ad9-172">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a><span data-ttu-id="14ad9-173">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="14ad9-173">Read data</span></span>
<span data-ttu-id="14ad9-174">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **seçin** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="14ad9-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="14ad9-175">Merhaba kod üç paketlerini içeri aktarır: Merhaba [sql paketi](https://golang.org/pkg/database/sql/), hello [pq paket](http://godoc.org/github.com/lib/pq) sürücü toocommunicate hello Postgres sunucu ve hello olarak [fmt paket](https://golang.org/pkg/fmt/) yazdırılması için Giriş ve çıkış hello komut satırında.</span><span class="sxs-lookup"><span data-stu-id="14ad9-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="14ad9-176">Merhaba kod yöntemi çağırır [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL ve denetimleri hello bağlantı yöntemini kullanarak veritabanı [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="14ad9-176">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="14ad9-177">A [veritabanı işleci](https://golang.org/pkg/database/sql/#DB) boyunca, hello bağlantı havuzu hello veritabanı sunucusu için bulunduran kullanılır.</span><span class="sxs-lookup"><span data-stu-id="14ad9-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="14ad9-178">Merhaba seçme sorgusu yöntemi çağrılarak çalıştırılır [db. Query()](https://golang.org/pkg/database/sql/#DB.Query), ve hello elde edilen satırları türünde bir değişken tutulur [satırları](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="14ad9-178">hello select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and hello resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="14ad9-179">Merhaba kod okur hello sütun veri değerlerini hello geçerli satırda yöntemini kullanarak [satır. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) ve döngüleri hello yineleyici kullanarak hello satırlarda üzerinden [satır. Next()](https://golang.org/pkg/database/sql/#Rows.Next) kadar daha fazla satır yok.</span><span class="sxs-lookup"><span data-stu-id="14ad9-179">hello code reads hello column data values in hello current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over hello rows using hello iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="14ad9-180">Her satırın sütun yazdırılan toohello konsol çıkışı değerlerdir. Her bir hata oluştu, özel checkError() yöntemi toocheck ve zaman bir hata oluşursa tooexit Panik.</span><span class="sxs-lookup"><span data-stu-id="14ad9-180">Each row's column values are printed toohello console out. Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="14ad9-181">Hello yerine `HOST`, `DATABASE`, `USER`, ve `PASSWORD` kendi değerlerinizi parametrelerle.</span><span class="sxs-lookup"><span data-stu-id="14ad9-181">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a><span data-ttu-id="14ad9-182">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="14ad9-182">Update data</span></span>
<span data-ttu-id="14ad9-183">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak veri güncelleştirme bir **güncelleştirme** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="14ad9-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="14ad9-184">Merhaba kod üç paketlerini içeri aktarır: Merhaba [sql paketi](https://golang.org/pkg/database/sql/), hello [pq paket](http://godoc.org/github.com/lib/pq) sürücü toocommunicate hello Postgres sunucu ve hello olarak [fmt paket](https://golang.org/pkg/fmt/) yazdırılması için Giriş ve çıkış hello komut satırında.</span><span class="sxs-lookup"><span data-stu-id="14ad9-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="14ad9-185">Merhaba kod yöntemi çağırır [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL ve denetimleri hello bağlantı yöntemini kullanarak veritabanı [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="14ad9-185">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="14ad9-186">A [veritabanı işleci](https://golang.org/pkg/database/sql/#DB) boyunca, hello bağlantı havuzu hello veritabanı sunucusu için bulunduran kullanılır.</span><span class="sxs-lookup"><span data-stu-id="14ad9-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="14ad9-187">Merhaba kod çağrıları hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) yöntemi toorun hello hello tablosunu güncelleştirir SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="14ad9-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="14ad9-188">Bir hata oluştu ve tooexit bir hata yoksa, Panik özel checkError() yöntemi toocheck ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="14ad9-188">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="14ad9-189">Hello yerine `HOST`, `DATABASE`, `USER`, ve `PASSWORD` kendi değerlerinizi parametrelerle.</span><span class="sxs-lookup"><span data-stu-id="14ad9-189">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="14ad9-190">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="14ad9-190">Delete data</span></span>
<span data-ttu-id="14ad9-191">Kullanım hello aşağıdaki tooconnect kod ve hello kullanarak verileri okuyun bir **silmek** SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="14ad9-191">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="14ad9-192">Merhaba kod üç paketlerini içeri aktarır: Merhaba [sql paketi](https://golang.org/pkg/database/sql/), hello [pq paket](http://godoc.org/github.com/lib/pq) sürücü toocommunicate hello Postgres sunucu ve hello olarak [fmt paket](https://golang.org/pkg/fmt/) yazdırılması için Giriş ve çıkış hello komut satırında.</span><span class="sxs-lookup"><span data-stu-id="14ad9-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="14ad9-193">Merhaba kod yöntemi çağırır [sql. Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure PostgreSQL ve denetimleri hello bağlantı yöntemini kullanarak veritabanı [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="14ad9-193">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="14ad9-194">A [veritabanı işleci](https://golang.org/pkg/database/sql/#DB) boyunca, hello bağlantı havuzu hello veritabanı sunucusu için bulunduran kullanılır.</span><span class="sxs-lookup"><span data-stu-id="14ad9-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="14ad9-195">Merhaba kod çağrıları hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) yöntemi toorun hello hello tablosunu güncelleştirir SQL deyimi.</span><span class="sxs-lookup"><span data-stu-id="14ad9-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="14ad9-196">Bir hata oluştu ve tooexit bir hata yoksa, Panik özel checkError() yöntemi toocheck ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="14ad9-196">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="14ad9-197">Hello yerine `HOST`, `DATABASE`, `USER`, ve `PASSWORD` kendi değerlerinizi parametrelerle.</span><span class="sxs-lookup"><span data-stu-id="14ad9-197">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="14ad9-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="14ad9-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="14ad9-199">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="14ad9-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
