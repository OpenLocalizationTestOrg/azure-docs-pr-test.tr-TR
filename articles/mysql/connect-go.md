---
title: "Go'yu kullanarak MySQL için Azure Veritabanı'na bağlanma | Microsoft Docs"
description: "Bu hızlı başlangıçta, MySQL için Azure Veritabanı'na bağlanmak ve buradan veri sorgulamak için kullanabileceğiniz birkaç Go kod örneği sağlanmıştır."
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
ms.openlocfilehash: 42a6b1c37de08971674c8b38f1e13bfd657f8b03
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="azure-database-for-mysql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="2f694-103">MySQL için Azure Veritabanı: Bağlanmak ve veri sorgulamak için Go dilini kullanma</span><span class="sxs-lookup"><span data-stu-id="2f694-103">Azure Database for MySQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="2f694-104">Bu hızlı başlangıçta, Windows, Ubuntu Linux ve Apple macOS platformlarından [Go](https://golang.org/) dilinde yazılmış kod kullanarak MySQL için Azure Veritabanı’na nasıl bağlanılacağı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2f694-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using code written in the [Go](https://golang.org/) language from Windows, Ubuntu Linux, and Apple macOS platforms.</span></span> <span data-ttu-id="2f694-105">Ayrıca veritabanında veri sorgulamak, eklemek, güncelleştirmek ve silmek için SQL deyimlerini nasıl kullanacağınız da gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2f694-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="2f694-106">Bu makalede, Go kullanarak geliştirmeyle ilgili bilgi sahibi olduğunuz ve MySQL için Azure Veritabanı ile çalışmaya yeni başladığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="2f694-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f694-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2f694-107">Prerequisites</span></span>
<span data-ttu-id="2f694-108">Bu hızlı başlangıçta, başlangıç noktası olarak şu kılavuzlardan birinde oluşturulan kaynaklar kullanılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="2f694-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2f694-109">Azure portalını kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f694-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="2f694-110">Azure CLI kullanarak MySQL için Azure Veritabanı sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f694-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-go-and-mysql-connector"></a><span data-ttu-id="2f694-111">Go ve MySQL bağlayıcısını yükleme</span><span class="sxs-lookup"><span data-stu-id="2f694-111">Install Go and MySQL connector</span></span>
<span data-ttu-id="2f694-112">Makinenize [Go](https://golang.org/doc/install) ve [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation)'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f694-112">Install [Go](https://golang.org/doc/install) and the [go-sql-driver for MySQL](https://github.com/go-sql-driver/mysql#installation) on your own machine.</span></span> <span data-ttu-id="2f694-113">Platformunuza bağlı olarak, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2f694-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="2f694-114">Windows</span><span class="sxs-lookup"><span data-stu-id="2f694-114">Windows</span></span>
1. <span data-ttu-id="2f694-115">[Yükleme yönergelerine](https://golang.org/doc/install) uygun olarak Microsoft Windows için Go’yu [indirin](https://golang.org/dl/) ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f694-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="2f694-116">Başlat menüsünden komut istemini başlatın.</span><span class="sxs-lookup"><span data-stu-id="2f694-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="2f694-117">Projeniz için şöyle bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f694-117">Make a folder for your project such.</span></span> <span data-ttu-id="2f694-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="2f694-118">`mkdir  %USERPROFILE%\go\src\mysqlgo`.</span></span>
4. <span data-ttu-id="2f694-119">Dizini değiştirerek proje klasörünüze geçin; örneğin, `cd %USERPROFILE%\go\src\mysqlgo`.</span><span class="sxs-lookup"><span data-stu-id="2f694-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\mysqlgo`.</span></span>
5. <span data-ttu-id="2f694-120">GOPATH için ortam değişkenini kaynak kod dizinine işaret edecek şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f694-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="2f694-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="2f694-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="2f694-122">`go get github.com/go-sql-driver/mysql` komutunu çalıştırarak [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation)'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f694-122">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="2f694-123">Özetle, Go’yu yükleyin ve ardından komut isteminde şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2f694-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="2f694-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="2f694-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="2f694-125">Bash kabuğunu başlatın.</span><span class="sxs-lookup"><span data-stu-id="2f694-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="2f694-126">`sudo apt-get install golang-go` komutunu çalıştırarak Go'yu yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f694-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="2f694-127">Giriş dizininizde projeniz için `mkdir -p ~/go/src/mysqlgo/` gibi bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f694-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="2f694-128">Dizini değiştirerek klasöre geçin; örneğin, `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="2f694-128">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="2f694-129">GOPATH ortam değişkenini geçerli bir kaynak dizine, örneğin geçerli giriş dizininizin go klasörüne işaret edecek şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f694-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="2f694-130">Bash kabuğunda `export GOPATH=~/go` komutunu çalıştırarak geçerli kabuk oturumu için GOPATH olarak go dizinini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f694-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="2f694-131">`go get github.com/go-sql-driver/mysql` komutunu çalıştırarak [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation)'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f694-131">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="2f694-132">Özetle, şu bash komutlarını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2f694-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a><span data-ttu-id="2f694-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="2f694-133">Apple macOS</span></span>
1. <span data-ttu-id="2f694-134">Platformunuza uygun [yükleme yönergelerine](https://golang.org/doc/install) göre Go’yu indirip yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f694-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="2f694-135">Bash kabuğunu başlatın.</span><span class="sxs-lookup"><span data-stu-id="2f694-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="2f694-136">Giriş dizininizde projeniz için `mkdir -p ~/go/src/mysqlgo/` gibi bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2f694-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/mysqlgo/`.</span></span>
4. <span data-ttu-id="2f694-137">Dizini değiştirerek klasöre geçin; örneğin, `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="2f694-137">Change directory into the folder, such as `cd ~/go/src/mysqlgo/`.</span></span>
5. <span data-ttu-id="2f694-138">GOPATH ortam değişkenini geçerli bir kaynak dizine, örneğin geçerli giriş dizininizin go klasörüne işaret edecek şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f694-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="2f694-139">Bash kabuğunda `export GOPATH=~/go` komutunu çalıştırarak geçerli kabuk oturumu için GOPATH olarak go dizinini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2f694-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="2f694-140">`go get github.com/go-sql-driver/mysql` komutunu çalıştırarak [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation)'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2f694-140">Install the [go-sql-driver for mysql](https://github.com/go-sql-driver/mysql#installation) by running the `go get github.com/go-sql-driver/mysql` command.</span></span>

   <span data-ttu-id="2f694-141">Özetle, Go’yu yükleyin ve ardından şu bash komutlarını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2f694-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a><span data-ttu-id="2f694-142">Bağlantı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="2f694-142">Get connection information</span></span>
<span data-ttu-id="2f694-143">MySQL için Azure Veritabanı'na bağlanmak üzere gereken bağlantı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="2f694-143">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="2f694-144">Tam sunucu adına ve oturum açma kimlik bilgilerine ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="2f694-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2f694-145">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2f694-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2f694-146">Azure portalında sol taraftaki menüden **Tüm kaynaklar**'a tıklayın ve oluşturduğunuz sunucuyu (örneğin, **myserver4demo**) arayın.</span><span class="sxs-lookup"><span data-stu-id="2f694-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="2f694-147">**myserver4demo** sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2f694-147">Click the server name **myserver4demo**.</span></span>
4. <span data-ttu-id="2f694-148">Sunucunun **Özellikler** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="2f694-148">Select the server's **Properties** page.</span></span> <span data-ttu-id="2f694-149">**Sunucu adını** ve **Sunucu yöneticisi oturum açma adını** not edin.</span><span class="sxs-lookup"><span data-stu-id="2f694-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="2f694-150">![MySQL için Azure Veritabanı - Sunucu Yöneticisi Oturum Açma](./media/connect-go/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="2f694-150">![Azure Database for MySQL - Server Admin Login](./media/connect-go/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="2f694-151">Sunucunuzun oturum açma bilgilerini unuttuysanız **Genel Bakış** sayfasına giderek Sunucu yöneticisi oturum açma adını görüntüleyin ve gerekirse parolayı sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="2f694-151">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>
   

## <a name="build-and-run-go-code"></a><span data-ttu-id="2f694-152">Go kodunu derleme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2f694-152">Build and run Go code</span></span> 
1. <span data-ttu-id="2f694-153">Golang kodlarını yazmak için Microsoft Windows’da Not Defteri , Ubuntu’da [VI](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) veya [Nano](https://www.nano-editor.org/), macOS’da TextEdit gibi basit metin düzenleyicilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f694-153">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="2f694-154">Daha zengin bir Tümleşik Geliştirme Ortamı (IDE) tercih ediyorsanız [Atom](https://atom.io/), Jetbrains [Gogland](https://www.jetbrains.com/go/) veya Microsoft [Visual Studio Code](https://code.visualstudio.com/) kullanmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f694-154">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="2f694-155">Aşağıdaki bölümde bulunan Go kodunu metin dosyalarına yapıştırın ve \*.go dosya uzantısıyla proje klasörünüze kaydedin; örneğin, Windows'da `%USERPROFILE%\go\src\mysqlgo\createtable.go` yolu veya Linux'ta `~/go/src/mysqlgo/createtable.go` yolu.</span><span class="sxs-lookup"><span data-stu-id="2f694-155">Paste the Go code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\mysqlgo\createtable.go` or Linux path `~/go/src/mysqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="2f694-156">Kodda `HOST`, `DATABASE`, `USER` ve `PASSWORD` sabitlerini bulun ve örnek değerleri kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f694-156">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span> 
4. <span data-ttu-id="2f694-157">Komut istemini veya bash kabuğunu başlatın.</span><span class="sxs-lookup"><span data-stu-id="2f694-157">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="2f694-158">Dizini değiştirerek proje klasörünüze geçin.</span><span class="sxs-lookup"><span data-stu-id="2f694-158">Change directory into your project folder.</span></span> <span data-ttu-id="2f694-159">Örneğin; Windows’da `cd %USERPROFILE%\go\src\mysqlgo\`.</span><span class="sxs-lookup"><span data-stu-id="2f694-159">For example, on Windows `cd %USERPROFILE%\go\src\mysqlgo\`.</span></span> <span data-ttu-id="2f694-160">Linux'ta `cd ~/go/src/mysqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="2f694-160">On Linux `cd ~/go/src/mysqlgo/`.</span></span>  <span data-ttu-id="2f694-161">Belirtilen IDE düzenleyicilerinden bazıları kabuk komutları gerektirmeden hata ayıklama ve çalışma zamanı özellikleri sunar.</span><span class="sxs-lookup"><span data-stu-id="2f694-161">Some of the IDE editors mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="2f694-162">Uygulamayı derlemek ve çalıştırmak için `go run createtable.go` komutunu yazarak kodu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2f694-162">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="2f694-163">Alternatif olarak, kodu yerel bir uygulamada derlemek için `go build createtable.go` komutunu kullanın, ardından uygulamayı çalıştırmak için `createtable.exe`’yi başlatın.</span><span class="sxs-lookup"><span data-stu-id="2f694-163">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="2f694-164">Bağlanma, tablo oluşturma ve veri ekleme</span><span class="sxs-lookup"><span data-stu-id="2f694-164">Connect, create table, and insert data</span></span>
<span data-ttu-id="2f694-165">Sunucuya bağlanmak, tablo oluşturmak ve **INSERT** SQL deyimini kullanarak verileri yüklemek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f694-165">Use the following code to connect to the server, create a table, and load the data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="2f694-166">Kod üç paketi içeri aktarır: [sql paketi](https://golang.org/pkg/database/sql/), MySQL için Azure Veritabanı'yla iletişim kuran sürücü olarak [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) ve komut satırında yazdırılan girdi ve çıktı için [fmt paketi](https://golang.org/pkg/fmt/).</span><span class="sxs-lookup"><span data-stu-id="2f694-166">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="2f694-167">Kod, [sql.Open()](http://go-database-sql.org/accessing.html) yöntemini çağırarak MySQL için Azure Veritabanı’na bağlanır ve [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) yöntemini kullanarak bağlantıyı kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="2f694-167">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="2f694-168">İşlem boyunca, veritabanı sunucusu için bağlantı havuzunu tutan bir [veritabanı tanıtıcı](https://golang.org/pkg/database/sql/#DB) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f694-168">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="2f694-169">Kod, birkaç DDL komutunu çalıştırmak için birkaç kez [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="2f694-169">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several DDL commands.</span></span> <span data-ttu-id="2f694-170">Kod ayrıca, hazırlanmış deyimleri farklı parametrelerle çalıştırıp üç satır eklemek için [Prepare()](http://go-database-sql.org/prepared.html) ve Exec() kullanır.</span><span class="sxs-lookup"><span data-stu-id="2f694-170">The code also uses the [Prepare()](http://go-database-sql.org/prepared.html) and Exec() to run prepared statements with different parameters to insert three rows.</span></span> <span data-ttu-id="2f694-171">Her seferinde hata oluşup olmadığını denetlemek ve acil çıkış yapmak için özel bir checkError() yöntemi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f694-171">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="2f694-172">`host`, `database`, `user` ve `password` sabitlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f694-172">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database.")

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

## <a name="read-data"></a><span data-ttu-id="2f694-173">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="2f694-173">Read data</span></span>
<span data-ttu-id="2f694-174">Bağlanmak ve **SELECT** SQL deyimi kullanarak verileri okumak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f694-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="2f694-175">Kod üç paketi içeri aktarır: [sql paketi](https://golang.org/pkg/database/sql/), MySQL için Azure Veritabanı'yla iletişim kuran sürücü olarak [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) ve komut satırında yazdırılan girdi ve çıktı için [fmt paketi](https://golang.org/pkg/fmt/).</span><span class="sxs-lookup"><span data-stu-id="2f694-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="2f694-176">Kod, [sql.Open()](http://go-database-sql.org/accessing.html) yöntemini çağırarak MySQL için Azure Veritabanı’na bağlanır ve [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) yöntemini kullanarak bağlantıyı kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="2f694-176">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="2f694-177">İşlem boyunca, veritabanı sunucusu için bağlantı havuzunu tutan bir [veritabanı tanıtıcı](https://golang.org/pkg/database/sql/#DB) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f694-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="2f694-178">Kod, seçme komutunu çalıştırmak için [Query()](https://golang.org/pkg/database/sql/#DB.Query) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="2f694-178">The code calls the [Query()](https://golang.org/pkg/database/sql/#DB.Query) method to run the select command.</span></span> <span data-ttu-id="2f694-179">Ardından, sonuç kümesi üzerinden yineleme yapmak için [Next()](https://golang.org/pkg/database/sql/#Rows.Next) ve sütun değerlerini ayrıştırıp değeri değişkenlere kaydetmek için [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="2f694-179">Then it runs [Next()](https://golang.org/pkg/database/sql/#Rows.Next) to iterate through the result set and [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) to parse the column values, saving the value into variables.</span></span> <span data-ttu-id="2f694-180">Her seferinde hata oluşup olmadığını denetlemek ve acil çıkış yapmak için özel bir checkError() yöntemi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f694-180">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="2f694-181">`host`, `database`, `user` ve `password` sabitlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f694-181">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from the table.
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

## <a name="update-data"></a><span data-ttu-id="2f694-182">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="2f694-182">Update data</span></span>
<span data-ttu-id="2f694-183">Bağlanmak ve **UPDATE** SQL deyimi kullanarak verileri güncelleştirmek için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f694-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="2f694-184">Kod üç paketi içeri aktarır: [sql paketi](https://golang.org/pkg/database/sql/), MySQL için Azure Veritabanı'yla iletişim kuran sürücü olarak [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) ve komut satırında yazdırılan girdi ve çıktı için [fmt paketi](https://golang.org/pkg/fmt/).</span><span class="sxs-lookup"><span data-stu-id="2f694-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="2f694-185">Kod, [sql.Open()](http://go-database-sql.org/accessing.html) yöntemini çağırarak MySQL için Azure Veritabanı’na bağlanır ve [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) yöntemini kullanarak bağlantıyı kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="2f694-185">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="2f694-186">İşlem boyunca, veritabanı sunucusu için bağlantı havuzunu tutan bir [veritabanı tanıtıcı](https://golang.org/pkg/database/sql/#DB) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f694-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="2f694-187">Kod, güncelleştirme komutunu çalıştırmak için [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="2f694-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the update command.</span></span> <span data-ttu-id="2f694-188">Her seferinde hata oluşup olmadığını denetlemek ve acil çıkış yapmak için özel bir checkError() yöntemi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f694-188">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="2f694-189">`host`, `database`, `user` ve `password` sabitlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f694-189">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a><span data-ttu-id="2f694-190">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="2f694-190">Delete data</span></span>
<span data-ttu-id="2f694-191">Bağlanmak ve **DELETE** SQL deyimini kullanarak verileri kaldırmak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f694-191">Use the following code to connect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="2f694-192">Kod üç paketi içeri aktarır: [sql paketi](https://golang.org/pkg/database/sql/), MySQL için Azure Veritabanı'yla iletişim kuran sürücü olarak [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) ve komut satırında yazdırılan girdi ve çıktı için [fmt paketi](https://golang.org/pkg/fmt/).</span><span class="sxs-lookup"><span data-stu-id="2f694-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [go sql driver for mysql](https://github.com/go-sql-driver/mysql#installation) as a driver to communicate with the Azure Database for MySQL, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="2f694-193">Kod, [sql.Open()](http://go-database-sql.org/accessing.html) yöntemini çağırarak MySQL için Azure Veritabanı’na bağlanır ve [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping) yöntemini kullanarak bağlantıyı kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="2f694-193">The code calls method [sql.Open()](http://go-database-sql.org/accessing.html) to connect to Azure Database for MySQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="2f694-194">İşlem boyunca, veritabanı sunucusu için bağlantı havuzunu tutan bir [veritabanı tanıtıcı](https://golang.org/pkg/database/sql/#DB) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f694-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="2f694-195">Kod, silme komutunu çalıştırmak için [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="2f694-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the delete command.</span></span> <span data-ttu-id="2f694-196">Her seferinde hata oluşup olmadığını denetlemek ve acil çıkış yapmak için özel bir checkError() yöntemi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2f694-196">Each time a custom checkError() method is used to check if an error occurred and panic to exit.</span></span>

<span data-ttu-id="2f694-197">`host`, `database`, `user` ve `password` sabitlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f694-197">Replace the `host`, `database`, `user`, and `password` constants with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a><span data-ttu-id="2f694-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2f694-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2f694-199">Dışarı Aktarma ve İçeri Aktarma seçeneğini kullanarak veritabanınızı geçirme</span><span class="sxs-lookup"><span data-stu-id="2f694-199">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
