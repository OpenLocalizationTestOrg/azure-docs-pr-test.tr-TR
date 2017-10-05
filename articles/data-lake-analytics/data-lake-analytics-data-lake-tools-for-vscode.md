---
title: "Azure Data Lake araçları: Kullanım Azure Data Lake araçları Visual Studio kodunu | Microsoft Docs"
description: "Visual Studio Code için Azure Data Lake araçları oluşturun, test ve U-SQL betikleri çalıştırmak için nasıl kullanılacağını öğrenin. "
Keywords: "VScode, Azure Data Lake araçları, yerel çalıştırma, yerel hata ayıklama, yerel hata ayıklama, Önizleme depolama dosyası, depolama birimi yolu için karşıya yükleme"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 833d14af47454a01fa3c97ffa854d688dd35871f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="2d597-104">Azure Data Lake araçları Visual Studio kodunu kullanın</span><span class="sxs-lookup"><span data-stu-id="2d597-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="2d597-105">U-SQL komut dosyalarını çalıştırmak ve Azure Data Lake araçları Visual Studio kodunu (VS Code) oluşturmak, sınamak için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="2d597-105">Learn how to use Azure Data Lake Tools for Visual Studio Code (VS Code) to create, test, and run U-SQL scripts.</span></span> <span data-ttu-id="2d597-106">Bilgiler aşağıdaki videoda da ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="2d597-106">The information is also covered in the following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="2d597-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2d597-107">Prerequisites</span></span>

<span data-ttu-id="2d597-108">Data Lake araçları, VS kodu tarafından desteklenen platformlarda yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2d597-108">Data Lake Tools can be installed on the platforms supported by VS Code.</span></span> <span data-ttu-id="2d597-109">Desteklenen platformlar, Windows, Linux ve MacOS içerir.</span><span class="sxs-lookup"><span data-stu-id="2d597-109">The supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="2d597-110">Farklı platformlarda aşağıdaki önkoşullara sahip:</span><span class="sxs-lookup"><span data-stu-id="2d597-110">The different platforms have the following prerequisites:</span></span>

- <span data-ttu-id="2d597-111">Windows</span><span class="sxs-lookup"><span data-stu-id="2d597-111">Windows</span></span>

    - <span data-ttu-id="2d597-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d597-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="2d597-113">[Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="2d597-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="2d597-114">Sistem ortam değişkeni yoluna java.exe yolunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2d597-114">Add the java.exe path to the system environment variable path.</span></span> <span data-ttu-id="2d597-115">Yapılandırma yönergeleri için bkz: [nasıl ayarlayın veya yol sistem değişkeni değiştirmeniz?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="2d597-115">For configuration instructions, see [How do I set or change the Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="2d597-116">Yol, C:\Program Files\Java\jdk1.8.0_77\jre\bin benzer.</span><span class="sxs-lookup"><span data-stu-id="2d597-116">The path is similar to C:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="2d597-117">[.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="2d597-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="2d597-118">Linux (Ubuntu 14.04 LTS önerilir)</span><span class="sxs-lookup"><span data-stu-id="2d597-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="2d597-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d597-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="2d597-120">Kod yüklemek için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="2d597-120">To install the code, enter the following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="2d597-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="2d597-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="2d597-122">Deb paket kaynağını güncelleştirmek için aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="2d597-122">To update the deb package source, enter the following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="2d597-123">Mono yüklemek için aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="2d597-123">To install Mono, enter the following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="2d597-124">Mono 4.6 desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="2d597-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="2d597-125">Tamamen 4.2.x yüklemeden önce sürüm 4.6 kaldırın.</span><span class="sxs-lookup"><span data-stu-id="2d597-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="2d597-126">[Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="2d597-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="2d597-127">Yükleme yönergeleri için bkz: [Linux 64 bit yükleme yönergeleri için Java]( https://java.com/en/download/help/linux_x64_install.xml) sayfası.</span><span class="sxs-lookup"><span data-stu-id="2d597-127">For instructions on installation, see the [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="2d597-128">[.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="2d597-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="2d597-129">macOS</span><span class="sxs-lookup"><span data-stu-id="2d597-129">MacOS</span></span>

    - <span data-ttu-id="2d597-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d597-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="2d597-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="2d597-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="2d597-132">[Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="2d597-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="2d597-133">Yükleme yönergeleri için bkz: [Linux 64 bit yükleme yönergeleri için Java](https://java.com/en/download/help/mac_install.xml) sayfası.</span><span class="sxs-lookup"><span data-stu-id="2d597-133">For instructions on installation, see the [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="2d597-134">[.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="2d597-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="2d597-135">Data Lake araçları yükleme</span><span class="sxs-lookup"><span data-stu-id="2d597-135">Install Data Lake Tools</span></span>

<span data-ttu-id="2d597-136">Önkoşulları yüklendikten sonra VS Code için Data Lake araçları yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d597-136">After you install the prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="2d597-137">**Data Lake araçları yüklemek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-137">**To install Data Lake Tools**</span></span>

1. <span data-ttu-id="2d597-138">Visual Studio Code'da açın.</span><span class="sxs-lookup"><span data-stu-id="2d597-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="2d597-139">CTRL + P seçin ve ardından aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="2d597-139">Select Ctrl+P, and then enter the following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="2d597-140">Visual Studio kod uzantılarının bir listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d597-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="2d597-141">Bunlardan biri olan **Azure Data Lake Araçları**.</span><span class="sxs-lookup"><span data-stu-id="2d597-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="2d597-142">Seçin **yükleme** yanına **Azure Data Lake Araçları**.</span><span class="sxs-lookup"><span data-stu-id="2d597-142">Select **Install** next to **Azure Data Lake Tools**.</span></span> <span data-ttu-id="2d597-143">Birkaç saniye sonra **yükleme** düğmesi değişiklikler **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="2d597-143">After a few seconds, the **Install** button changes to **Reload**.</span></span>
4. <span data-ttu-id="2d597-144">Seçin **yeniden** uzantısını etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2d597-144">Select **Reload** to activate the extension.</span></span>
5. <span data-ttu-id="2d597-145">Seçin **Tamam** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="2d597-145">Select **OK** to confirm.</span></span> <span data-ttu-id="2d597-146">Azure Data Lake araçları içinde gördüğünüz **uzantıları** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="2d597-146">You can see Azure Data Lake Tools in the **Extensions** pane.</span></span>
    <span data-ttu-id="2d597-147">![Visual Studio kod uzantılarını bölmesi için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="2d597-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="2d597-148">Azure Data Lake araçları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="2d597-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="2d597-149">Yeni bir .usql dosyası oluşturun veya uzantıyı etkinleştirmek için mevcut bir .usql dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="2d597-149">Create a new .usql file or open an existing .usql file to activate the extension.</span></span> 

## <a name="connect-to-azure"></a><span data-ttu-id="2d597-150">Azure'a Bağlanma</span><span class="sxs-lookup"><span data-stu-id="2d597-150">Connect to Azure</span></span>

<span data-ttu-id="2d597-151">Derleme ve Data Lake Analytics U-SQL betikleri çalıştırmak için önce Azure hesabınızda bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d597-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect to your Azure account.</span></span>

<span data-ttu-id="2d597-152">**Azure'a bağlanmak için**</span><span class="sxs-lookup"><span data-stu-id="2d597-152">**To connect to Azure**</span></span>

1.  <span data-ttu-id="2d597-153">Komut paletini açmak için Ctrl + Shift + P seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-153">Select Ctrl+Shift+P to open the command palette.</span></span> 
2.  <span data-ttu-id="2d597-154">Girin **ADL: oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="2d597-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="2d597-155">Oturum açma bilgileri görünür **çıkış** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="2d597-155">The login information appears in the **Output** pane.</span></span>

    <span data-ttu-id="2d597-156">![Data Lake araçları Visual Studio Code komutu paletini](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Visual Studio Code cihaz oturum açma bilgileri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="2d597-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="2d597-157">Seçin CTRL + üzerinde oturum açma URL'Sİ'ı tıklatın: oturum açma Web sayfası açmak için https://aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="2d597-157">Select Ctrl+click on the login URL: https://aka.ms/devicelogin to open the login webpage.</span></span> <span data-ttu-id="2d597-158">Kodu girin **G567LX42V** metin kutusuna yazın ve ardından **devam**.</span><span class="sxs-lookup"><span data-stu-id="2d597-158">Enter the code **G567LX42V** into the text box, and then select **Continue**.</span></span>

   ![Visual Studio Code oturum açma için Data Lake araçları kodu yapıştırın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="2d597-160">Web sayfasından oturum açmak için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="2d597-160">Follow the instructions to sign in from the webpage.</span></span> <span data-ttu-id="2d597-161">Bağlandığınızda, Azure hesap adınızı sol alt köşesindeki durum çubuğunda görünür **VS Code** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2d597-161">When you're connected, your Azure account name appears on the status bar in the lower-left corner of the **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="2d597-162">İki etmen etkin hesabınız varsa, PIN kullanmak yerine telefon kimlik doğrulaması kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2d597-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="2d597-163">Oturumu kapatmak için aşağıdaki komutu girin **ADL: oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="2d597-163">To sign out, enter the command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="2d597-164">Data Lake Analytics hesaplarını listeler</span><span class="sxs-lookup"><span data-stu-id="2d597-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="2d597-165">Bağlantıyı sınamak için Data Lake Analytics hesaplarının bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="2d597-165">To test the connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="2d597-166">**Azure aboneliğinizin Data Lake Analytics hesaplarla listelemek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-166">**To list the Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="2d597-167">Komut paletini açmak için Ctrl + Shift + P seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-167">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="2d597-168">Girin **ADL: liste hesapları**.</span><span class="sxs-lookup"><span data-stu-id="2d597-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="2d597-169">Hesapları görünür **çıkış** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="2d597-169">The accounts appear in the **Output** pane.</span></span>

## <a name="open-the-sample-script"></a><span data-ttu-id="2d597-170">Örnek komut dosyasını açın</span><span class="sxs-lookup"><span data-stu-id="2d597-170">Open the sample script</span></span>
<span data-ttu-id="2d597-171">Komut palet (Ctrl + Shift + P) açın ve girin **ADL: açık örnek komut dosyası**.</span><span class="sxs-lookup"><span data-stu-id="2d597-171">Open the command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="2d597-172">Bu örnek başka bir örneği açılır.</span><span class="sxs-lookup"><span data-stu-id="2d597-172">This opens another instance of this sample.</span></span> <span data-ttu-id="2d597-173">Ayrıca düzenleyebilir, yapılandırmak ve bu örnek komut gönderme.</span><span class="sxs-lookup"><span data-stu-id="2d597-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="2d597-174">U-SQL ile çalışma</span><span class="sxs-lookup"><span data-stu-id="2d597-174">Work with U-SQL</span></span>

<span data-ttu-id="2d597-175">U-SQL dosya veya U-SQL ile çalışmak için bir klasör açın.</span><span class="sxs-lookup"><span data-stu-id="2d597-175">You need open either a U-SQL file or a folder to work with U-SQL.</span></span>

<span data-ttu-id="2d597-176">**U-SQL projeniz için bir klasör açmak için**</span><span class="sxs-lookup"><span data-stu-id="2d597-176">**To open a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="2d597-177">Visual Studio koddan seçin **dosya** menüsüne ve ardından **Klasör Aç**.</span><span class="sxs-lookup"><span data-stu-id="2d597-177">From Visual Studio Code, select the **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="2d597-178">Bir klasör belirtin ve ardından **Klasör Seç**.</span><span class="sxs-lookup"><span data-stu-id="2d597-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="2d597-179">Seçin **dosya** menüsüne ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="2d597-179">Select the **File** menu, and then select **New**.</span></span> <span data-ttu-id="2d597-180">Adsız-1 dosyası projeye eklenir.</span><span class="sxs-lookup"><span data-stu-id="2d597-180">An Untitled-1 file is added to the project.</span></span>
4. <span data-ttu-id="2d597-181">Adsız-1 dosyasına aşağıdaki kodu girin:</span><span class="sxs-lookup"><span data-stu-id="2d597-181">Enter the following code into the Untitled-1 file:</span></span>

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    <span data-ttu-id="2d597-182">Komut dosyası/Output klasöründe bulunan bazı veriler içeren bir departments.csv dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2d597-182">The script creates a departments.csv file with some data included in the /output folder.</span></span>

5. <span data-ttu-id="2d597-183">Dosyayı Farklı Kaydet **myUSQL.usql** açılan klasörde.</span><span class="sxs-lookup"><span data-stu-id="2d597-183">Save the file as **myUSQL.usql** in the opened folder.</span></span> <span data-ttu-id="2d597-184">Bir adltools_settings.json yapılandırma dosyası projeye de eklenir.</span><span class="sxs-lookup"><span data-stu-id="2d597-184">A adltools_settings.json configuration file is also added to the project.</span></span>
4. <span data-ttu-id="2d597-185">Açın ve aşağıdaki özelliklere sahip adltools_settings.json yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="2d597-185">Open and configure adltools_settings.json with the following properties:</span></span>

    - <span data-ttu-id="2d597-186">: Bir Data Lake Analytics hesabı, Azure aboneliğinizin altında.</span><span class="sxs-lookup"><span data-stu-id="2d597-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="2d597-187">Veritabanı: Hesabınız altındaki bir veritabanı.</span><span class="sxs-lookup"><span data-stu-id="2d597-187">Database: A database under your account.</span></span> <span data-ttu-id="2d597-188">Varsayılan değer **ana**.</span><span class="sxs-lookup"><span data-stu-id="2d597-188">The default is **master**.</span></span>
    - <span data-ttu-id="2d597-189">Şema: Veritabanınızı altında bir şema.</span><span class="sxs-lookup"><span data-stu-id="2d597-189">Schema: A schema under your database.</span></span> <span data-ttu-id="2d597-190">Varsayılan değer **dbo**.</span><span class="sxs-lookup"><span data-stu-id="2d597-190">The default is **dbo**.</span></span>
    - <span data-ttu-id="2d597-191">İsteğe bağlı ayarlar:</span><span class="sxs-lookup"><span data-stu-id="2d597-191">Optional settings:</span></span>
        - <span data-ttu-id="2d597-192">Öncelik: Öncelik 1 ile-1 ile 1000 en yüksek öncelikli olarak aralıktır.</span><span class="sxs-lookup"><span data-stu-id="2d597-192">Priority: The priority range is from 1 to 1000 with 1 as the highest priority.</span></span> <span data-ttu-id="2d597-193">Varsayılan değer **1000**.</span><span class="sxs-lookup"><span data-stu-id="2d597-193">The default value is **1000**.</span></span>
        - <span data-ttu-id="2d597-194">Paralellik: Paralellik 1 ila 150 için aralıktır.</span><span class="sxs-lookup"><span data-stu-id="2d597-194">Parallelism: The parallelism range is from 1 to 150.</span></span> <span data-ttu-id="2d597-195">Azure Data Lake Analytics hesabınızı izin verilen maksimum paralellik varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="2d597-195">The default value is the maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="2d597-196">Ayarları geçersiz varsa, varsayılan değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2d597-196">If the settings are invalid, the default values are used.</span></span>

    ![Visual Studio Code yapılandırma dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="2d597-198">İşlem Data Lake Analytics hesabı derlemek ve U-SQL işleri çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2d597-198">A compute Data Lake Analytics account is needed to compile and run U-SQL jobs.</span></span> <span data-ttu-id="2d597-199">Derleme ve U-SQL işleri çalıştırma önce bilgisayar hesabını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d597-199">You must configure the computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="2d597-200">Yapılandırma kaydedildikten sonra hesap, veritabanı ve şema bilgilerini karşılık gelen .usql dosyası sol alt köşesindeki durum çubuğunda görünür.</span><span class="sxs-lookup"><span data-stu-id="2d597-200">After the configuration is saved, the account, database, and schema information appears on the status bar at the bottom-left corner of the corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="2d597-201">Yapabilecekleriniz bir klasörü açtığınızda, bir dosyanın açılması için karşılaştırıldığında:</span><span class="sxs-lookup"><span data-stu-id="2d597-201">Compared to opening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="2d597-202">Arka plan kodu dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="2d597-202">Use a code-behind file.</span></span> <span data-ttu-id="2d597-203">Tek dosya modunda arka plan kodu desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="2d597-203">In the single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="2d597-204">Bir yapılandırma dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="2d597-204">Use a configuration file.</span></span> <span data-ttu-id="2d597-205">Bir klasörü açtığınızda, çalışma klasörü komut tek yapılandırma dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="2d597-205">When you open a folder, the scripts in the working folder share a single configuration file.</span></span>


<span data-ttu-id="2d597-206">U-SQL betiği Data Lake Analytics hizmeti aracılığıyla uzaktan derler.</span><span class="sxs-lookup"><span data-stu-id="2d597-206">The U-SQL script compiles remotely through the Data Lake Analytics service.</span></span> <span data-ttu-id="2d597-207">Çıkarırsanız **derleme** komutu, U-SQL betiği, Data Lake Analytics hesabınızı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2d597-207">When you issue the **compile** command, the U-SQL script is sent to your Data Lake Analytics account.</span></span> <span data-ttu-id="2d597-208">Daha sonra Visual Studio Code derleme sonucu alır.</span><span class="sxs-lookup"><span data-stu-id="2d597-208">Later, Visual Studio Code receives the compilation result.</span></span> <span data-ttu-id="2d597-209">Uzak derleme nedeniyle, Data Lake Analytics hesabınızı yapılandırma dosyasındaki bağlanma bilgilerini listesinde Visual Studio Code gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2d597-209">Due to the remote compilation, Visual Studio Code requires that you list the information to connect to your Data Lake Analytics account in the configuration file.</span></span>

<span data-ttu-id="2d597-210">**U-SQL betiği derlemek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-210">**To compile a U-SQL script**</span></span>

1. <span data-ttu-id="2d597-211">Komut paletini açmak için Ctrl + Shift + P seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-211">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="2d597-212">Girin **ADL: derleme betik**.</span><span class="sxs-lookup"><span data-stu-id="2d597-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="2d597-213">Derleme sonuçları görünür **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2d597-213">The compile results appear in the **Output** window.</span></span> <span data-ttu-id="2d597-214">Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: derleme betik** bir U-SQL işi derlemek için.</span><span class="sxs-lookup"><span data-stu-id="2d597-214">You can also right-click a script file, and then select **ADL: Compile Script** to compile a U-SQL job.</span></span> <span data-ttu-id="2d597-215">Derleme sonucu görünür **çıkış** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="2d597-215">The compilation result appears in the **Output** pane.</span></span>
 

<span data-ttu-id="2d597-216">**U-SQL betiği göndermek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-216">**To submit a U-SQL script**</span></span>

1. <span data-ttu-id="2d597-217">Komut paletini açmak için Ctrl + Shift + P seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-217">Select Ctrl+Shift+P to open the command palette.</span></span> 
2. <span data-ttu-id="2d597-218">Girin **ADL: işi göndermek**.</span><span class="sxs-lookup"><span data-stu-id="2d597-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="2d597-219">Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: işi Gönder**.</span><span class="sxs-lookup"><span data-stu-id="2d597-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="2d597-220">U-SQL işi gönderdikten sonra gönderme günlükleri görünür **çıkış** VS Code penceresinde.</span><span class="sxs-lookup"><span data-stu-id="2d597-220">After you submit a U-SQL job, the submission logs appear in the **Output** window in VS Code.</span></span> <span data-ttu-id="2d597-221">Gönderim başarılı olursa, proje URL'si de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2d597-221">If the submission is successful, the job URL appears as well.</span></span> <span data-ttu-id="2d597-222">Proje URL'si gerçek zamanlı iş durumunu izlemek için bir web tarayıcısı açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d597-222">You can open the job URL in a web browser to track the real-time job status.</span></span>

<span data-ttu-id="2d597-223">İş ayrıntılarını çıktısını etkinleştirmek için ayarlanmış **jobInformationOutputPath** içinde **vs code için u sql_settings.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="2d597-223">To enable the output of the job details, set **jobInformationOutputPath** in the **vs code for the u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="2d597-224">Bir arka plan kod dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="2d597-224">Use a code-behind file</span></span>

<span data-ttu-id="2d597-225">Tek bir U-SQL betiği ile ilişkili bir C# dosyasına bir arka plan kodu dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="2d597-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="2d597-226">UDO, UDA, UDT ve arka plan kod dosyasına UDF için adanmış bir komut dosyası tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d597-226">You can define a script dedicated to UDO, UDA, UDT, and UDF in the code-behind file.</span></span> <span data-ttu-id="2d597-227">UDO, UDA, UDT ve UDF doğrudan komut dosyası derleme ilk kaydettirmeden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2d597-227">The UDO, UDA, UDT, and UDF can be used directly in the script without registering the assembly first.</span></span> <span data-ttu-id="2d597-228">Kendi eşleme U-SQL komut dosyası ile aynı klasörde arka plan kod dosyasına yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="2d597-228">The code-behind file is put in the same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="2d597-229">Komut dosyası xxx.usql olarak adlandırılmışsa, arka plan kodu xxx.usql.cs adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="2d597-229">If the script is named xxx.usql, the code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="2d597-230">Arka plan kodu dosyasını el ile silin, arka plan kodu özelliği, ilişkili U-SQL betiği için devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="2d597-230">If you manually delete the code-behind file, the code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="2d597-231">U-SQL betiği için müşteri kod yazma hakkında daha fazla bilgi için bkz: [yazma ve özel kodda kullanarak U-SQL: kullanıcı tanımlı işlevler]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="2d597-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="2d597-232">Arka plan kodu desteklemek için bir çalışma klasörü açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d597-232">To support code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="2d597-233">**Bir arka plan kod dosyası oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="2d597-233">**To generate a code-behind file**</span></span>

1. <span data-ttu-id="2d597-234">Bir kaynak dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="2d597-234">Open a source file.</span></span> 
2. <span data-ttu-id="2d597-235">Komut paletini açmak için Ctrl + Shift + P seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-235">Select Ctrl+Shift+P to open the command palette.</span></span>
3. <span data-ttu-id="2d597-236">Girin **ADL: arka plan kod oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="2d597-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="2d597-237">Arka plan kod dosyası, aynı klasörde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2d597-237">A code-behind file is created in the same folder.</span></span> 

<span data-ttu-id="2d597-238">Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: kod arkasında oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="2d597-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="2d597-239">Derleme ve U-SQL betiği bir arka plan kodu dosya göndermek için tek başına U-SQL betiği ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="2d597-239">To compile and submit a U-SQL script with a code-behind file is the same as with the standalone U-SQL script file.</span></span>

<span data-ttu-id="2d597-240">Aşağıdaki iki ekran görüntüleri bir arka plan kod dosyası ve onun ilişkili U-SQL komut dosyası gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="2d597-240">The following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Visual Studio Code arka plan kod için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Visual Studio Code arka plan kodu komut dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="2d597-243">Derlemeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="2d597-243">Use assemblies</span></span>

<span data-ttu-id="2d597-244">Derlemeler geliştirme hakkında daha fazla bilgi için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="2d597-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="2d597-245">Data Lake araçları, Data Lake Analytics Kataloğu'nda özel kod derlemeleri kaydetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d597-245">You can use Data Lake Tools to register custom code assemblies in the Data Lake Analytics catalog.</span></span>

<span data-ttu-id="2d597-246">**Bir derlemeyi kaydetmek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-246">**To register an assembly**</span></span>

<span data-ttu-id="2d597-247">Derleme aracılığıyla kaydedebilirsiniz **ADL: kaydetmek derleme** veya **ADL: kaydetmek derleme yapılandırma yoluyla** komutları.</span><span class="sxs-lookup"><span data-stu-id="2d597-247">You can register the assembly through the **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="2d597-248">**ADL kaydetmek için: kayıt derleme komutu**</span><span class="sxs-lookup"><span data-stu-id="2d597-248">**To register through the ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="2d597-249">Komut paletini açmak için Ctrl + Shift + P seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-249">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="2d597-250">Girin **ADL: kaydetmek derleme**.</span><span class="sxs-lookup"><span data-stu-id="2d597-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="2d597-251">Yerel derleme yolu belirtin.</span><span class="sxs-lookup"><span data-stu-id="2d597-251">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="2d597-252">Bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="2d597-253">Bir veritabanı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-253">Select a database.</span></span>

<span data-ttu-id="2d597-254">Sonuçları: Portal bir tarayıcıda açıldığından ve derleme kayıt işlemi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2d597-254">Results: The portal is opened in a browser and displays the assembly registration process.</span></span>  

<span data-ttu-id="2d597-255">Tetiklemek için kullanışlı bir başka yolu **ADL: kaydetmek derleme** komuttur dosya Gezgini'nde .dll dosyasını sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2d597-255">Another convenient way to trigger the **ADL: Register Assembly** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="2d597-256">**ADL yine de kaydetmek için: kayıt derleme yapılandırma komutu**</span><span class="sxs-lookup"><span data-stu-id="2d597-256">**To register though the ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="2d597-257">Komut paletini açmak için Ctrl + Shift + P seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-257">Select Ctrl+Shift+P to open the command palette.</span></span>
2.  <span data-ttu-id="2d597-258">Girin **ADL: kaydetmek derleme yapılandırma yoluyla**.</span><span class="sxs-lookup"><span data-stu-id="2d597-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="2d597-259">Yerel derleme yolu belirtin.</span><span class="sxs-lookup"><span data-stu-id="2d597-259">Specify the local assembly path.</span></span> 
4.  <span data-ttu-id="2d597-260">JSON dosyası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2d597-260">The JSON file is displayed.</span></span> <span data-ttu-id="2d597-261">Gözden geçirin ve kaynak parametreleri ve derleme bağımlılıklar gerekiyorsa düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="2d597-261">Review and edit the assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="2d597-262">Yönergeler görüntülenir **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2d597-262">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="2d597-263">Derleme kayıt aşamasına ilerlemek için (Ctrl + S) JSON dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2d597-263">To proceed to the assembly registration, save (Ctrl+S) the JSON file.</span></span>

![Visual Studio Code arka plan kod için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="2d597-265">Derleme bağımlılıkları: Azure Data Lake araçları autodetects DLL bağımlılıkları sahip olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="2d597-265">Assembly dependencies: Azure Data Lake Tools autodetects whether the DLL has any dependencies.</span></span> <span data-ttu-id="2d597-266">Algılandıkları sonra bağımlılıkları JSON dosyasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2d597-266">The dependencies are displayed in the JSON file after they are detected.</span></span> 
>- <span data-ttu-id="2d597-267">Kaynaklar: Derleme kaydı bir parçası olarak, DLL kaynakları (örneğin, .txt, .png ve .csv) karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="2d597-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of the assembly registration.</span></span> 

<span data-ttu-id="2d597-268">Tetiklemek için başka bir yolu **ADL: kaydetmek derleme yapılandırma yoluyla** komuttur dosya Gezgini'nde .dll dosyasını sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2d597-268">Another way to trigger the **ADL: Register Assembly through Configuration** command is to right-click the .dll file in File Explorer.</span></span> 

<span data-ttu-id="2d597-269">Aşağıdaki U-SQL kodu, bütünleştirilmiş çağırmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2d597-269">The following U-SQL code demonstrates how to call an assembly.</span></span> <span data-ttu-id="2d597-270">Örnekte, derleme adı: *test*.</span><span class="sxs-lookup"><span data-stu-id="2d597-270">In the sample, the assembly name is *test*.</span></span>

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    TO @"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-the-data-lake-analytics-catalog"></a><span data-ttu-id="2d597-271">Data Lake Analytics Kataloğu'na erişme</span><span class="sxs-lookup"><span data-stu-id="2d597-271">Access the Data Lake Analytics catalog</span></span>

<span data-ttu-id="2d597-272">Azure'a bağlandıktan sonra U-SQL Kataloğu'na erişmek için aşağıdaki adımları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d597-272">After you have connected to Azure, you can use the following steps to access the U-SQL catalog.</span></span>

<span data-ttu-id="2d597-273">**Azure Data Lake Analytics meta verilerine erişmek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-273">**To access the Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="2d597-274">Ctrl + Shift + P seçin ve ardından girin **ADL: liste tabloları**.</span><span class="sxs-lookup"><span data-stu-id="2d597-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="2d597-275">Data Lake Analytics hesaplardan birini seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-275">Select one of the Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="2d597-276">Data Lake Analytics veritabanlarından birini seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-276">Select one of the Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="2d597-277">Şemalar birini seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-277">Select one of the schemas.</span></span> <span data-ttu-id="2d597-278">Tabloların listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d597-278">You can see the list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="2d597-279">Görünüm Data Lake Analytics işleri</span><span class="sxs-lookup"><span data-stu-id="2d597-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="2d597-280">**Data Lake Analytics işleri görüntülemek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-280">**To view Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="2d597-281">Komut palet (Ctrl + Shift + P) açın ve seçin **ADL: Göster iş**.</span><span class="sxs-lookup"><span data-stu-id="2d597-281">Open the command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="2d597-282">Bir Data Lake Analytics veya yerel bir hesap seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="2d597-283">İşleri listesini görünmesi hesabı için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2d597-283">Wait for the jobs list for the account to appear.</span></span>
4.  <span data-ttu-id="2d597-284">İş listesinden bir iş seçin, Data Lake araçları Azure Portalı'nda iş ayrıntılarını açar ve VS Code'da iş tanımı dosyası gösterir.</span><span class="sxs-lookup"><span data-stu-id="2d597-284">Select a job from job list, Data Lake Tools opens the job details in the Azure portal and displays the JobInfo file in VS Code.</span></span>

![Visual Studio kod IntelliSense nesne türleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="2d597-286">Azure Data Lake Storage tümleştirme</span><span class="sxs-lookup"><span data-stu-id="2d597-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="2d597-287">Azure Data Lake Store ile ilgili komutları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2d597-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="2d597-288">Azure Data Lake Storage kaynaklara göz atın.</span><span class="sxs-lookup"><span data-stu-id="2d597-288">Browse through the Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="2d597-289">Azure Data Lake Storage dosyanın önizlemesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="2d597-289">Preview the Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="2d597-290">VS code'da Azure Data Lake Storage için doğrudan dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2d597-290">Upload the file directly to Azure Data Lake Storage in VS Code.</span></span> 

### <a name="list-the-storage-path"></a><span data-ttu-id="2d597-291">Depolama alanı yolu listesi</span><span class="sxs-lookup"><span data-stu-id="2d597-291">List the storage path</span></span> 
<span data-ttu-id="2d597-292">Depolama alanı yolu komut palet ya da sağ tıklatma listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d597-292">You can list the storage path through the command palette or through right-click.</span></span>

<span data-ttu-id="2d597-293">**Komut palet depolama yolundan listelemek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-293">**To list the storage path through the command palette**</span></span>

1.  <span data-ttu-id="2d597-294">Komut palet (Ctrl + Shift + P) açın ve girin **ADL: listesi depolama yolu**.</span><span class="sxs-lookup"><span data-stu-id="2d597-294">Open the command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Visual Studio Code listesi depolama birimi yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="2d597-296">Depolama alanı yolu listeleme, tercih edilen yol seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-296">Select your preferred way for listing the storage path.</span></span> <span data-ttu-id="2d597-297">Bu oluşturularak kullanan **bir yol girin** bir örnek olarak.</span><span class="sxs-lookup"><span data-stu-id="2d597-297">This passage uses **Enter a path** as an example.</span></span>

    ![Visual Studio Code depolama yolu listesine bir yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="2d597-299">VS Code her Data Lake Analytics hesabı son ziyaret edilen yolu tutar.</span><span class="sxs-lookup"><span data-stu-id="2d597-299">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="2d597-300">Örneğin: / tt/sn.</span><span class="sxs-lookup"><span data-stu-id="2d597-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="2d597-301">Kök yolu tarayıcısından: Seçili Data Lake Analytics hesabınızı veya yerel bir yol listesi kök yolu.</span><span class="sxs-lookup"><span data-stu-id="2d597-301">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="2d597-302">Bir yol girin: Seçili Data Lake Analytics hesabınızı belirtilen yoldan veya yerel bir yol listesi.</span><span class="sxs-lookup"><span data-stu-id="2d597-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="2d597-303">Bir hesap, yerel yol veya bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-303">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Daha fazla bilgi için Visual Studio Code Data Lake araçları seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="2d597-305">Seçin **daha fazla** daha fazla Data Lake Analytics hesaplarını listelemek ve Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-305">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="2d597-307">Bir Azure depolama yolunu girin.</span><span class="sxs-lookup"><span data-stu-id="2d597-307">Enter an Azure storage path.</span></span> <span data-ttu-id="2d597-308">Örneğin, / çıktı.</span><span class="sxs-lookup"><span data-stu-id="2d597-308">For example, /output.</span></span>

    ![Data Lake araçları Visual Studio Code için depolama alanı yolu girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="2d597-310">Sonuçları: Komutu palet girişlerini temel yol bilgileri listeler.</span><span class="sxs-lookup"><span data-stu-id="2d597-310">Results: The command palette lists the path information based on your entries.</span></span>

    ![Data Lake araçları Visual Studio Code için depolama birimi yolu sonuçları listesi](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="2d597-312">Sağ bağlam menüsü göreli yolu listelemek için daha kullanışlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="2d597-312">A more convenient way to list the relative path is through the right-click context menu.</span></span>

<span data-ttu-id="2d597-313">**Sağ depolama yolundan listelemek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-313">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="2d597-314">Seçmek için yol dizesi sağ **listesi depolama yolu**.</span><span class="sxs-lookup"><span data-stu-id="2d597-314">Right-click the path string to select **List Storage Path**.</span></span>

       ![Visual Studio Code için Data Lake Araçları bağlam menüsü sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="2d597-316">Seçilen göreli yol komutu palette görünür.</span><span class="sxs-lookup"><span data-stu-id="2d597-316">The selected relative path appears in the command palette.</span></span>

   ![Data Lake araçları Visual Studio Code seçili göreli yolu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="2d597-318">Bir hesap, yerel yol veya bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-318">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="2d597-320">Sonuçları: Komutu palet geçerli yolu için dosya ve klasörleri listeler.</span><span class="sxs-lookup"><span data-stu-id="2d597-320">Results: The command palette lists the folders and files for the current path.</span></span>

       ![Visual Studio Code listeden geçerli yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-the-storage-file"></a><span data-ttu-id="2d597-322">Depolama dosya önizleme</span><span class="sxs-lookup"><span data-stu-id="2d597-322">Preview the storage file</span></span>
<span data-ttu-id="2d597-323">Depolama dosyası komutu palet ya da sağ tıklatma önizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d597-323">You can preview the storage file through the command palette or through right-click.</span></span>

<span data-ttu-id="2d597-324">**Depolama dosyası komutu palet aracılığıyla önizlemek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-324">**To preview the storage file through the command palette**</span></span>

1.  <span data-ttu-id="2d597-325">Komut palet (Ctrl + Shift + P) açın ve girin **ADL: Önizleme depolama dosyası**.</span><span class="sxs-lookup"><span data-stu-id="2d597-325">Open the command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Visual Studio Code Önizleme depolama dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="2d597-327">Bir hesap, yerel yol veya bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-327">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Visual Studio Code için Data Lake araçları hesabı listesi](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="2d597-329">Seçin **daha fazla** daha fazla Data Lake Analytics hesaplarını listelemek ve Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-329">Select **more** to list more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="2d597-331">Bir Azure depolama alanı yolu veya dosya girin.</span><span class="sxs-lookup"><span data-stu-id="2d597-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="2d597-332">Örneğin, /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="2d597-332">For example, /output/SearchLog.txt.</span></span>

       ![Data Lake araçları Visual Studio Code için depolama birimi yolu ve dosya girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="2d597-334">Sonuçları: Komutu palet girişlerini temel yol bilgileri listeler.</span><span class="sxs-lookup"><span data-stu-id="2d597-334">Results: The command palette lists the path information based on your entries.</span></span>

       ![Visual Studio Code için Data Lake araçları dosya sonucu Önizleme](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="2d597-336">**Sağ depolama yolundan listelemek için**</span><span class="sxs-lookup"><span data-stu-id="2d597-336">**To list the storage path through right-click**</span></span>

1.  <span data-ttu-id="2d597-337">Bir dosyayı önizlemek için dosya yolu sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2d597-337">To preview a file, right-click the file path.</span></span>

   ![Visual Studio Code için Data Lake Araçları bağlam menüsü sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="2d597-339">Bir hesap, yerel yol veya bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-339">Select an account from the local path or a Data Lake Analytics account.</span></span>

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="2d597-341">Sonuçları: VS Code dosya önizleme sonuçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2d597-341">Results: VS Code displays the preview results of the file.</span></span>

       ![Visual Studio Code için Data Lake araçları dosya sonucu Önizleme](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="2d597-343">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="2d597-343">Upload a file</span></span> 

<span data-ttu-id="2d597-344">Komutları girerek dosyaları karşıya yükleyebilir **ADL: dosyasını karşıya yükle** veya **ADL: yapılandırma yoluyla dosyasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="2d597-344">You can upload files by entering the commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="2d597-345">**Karşıya yüklemek için yine de ADL dosyaları: karşıya dosya komutu**</span><span class="sxs-lookup"><span data-stu-id="2d597-345">**To upload files though the ADL: Upload File command**</span></span>
1. <span data-ttu-id="2d597-346">Komut paletini açmak veya komut dosyası Düzenleyicisi'ni sağ tıklatın ve ardından girin için Ctrl + Shift + P seçin **dosyasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="2d597-346">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="2d597-347">Dosyayı karşıya yüklemek için yerel bir yol girin.</span><span class="sxs-lookup"><span data-stu-id="2d597-347">To upload the file, enter a local path.</span></span>

    ![Visual Studio Code için Data Lake araçları yerel yolu girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="2d597-349">Depolama alanı yolu listeleme yöntemlerden birini seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-349">Select one of the ways of listing the storage path.</span></span> <span data-ttu-id="2d597-350">Bu oluşturularak kullanan **bir yol girin** bir örnek olarak.</span><span class="sxs-lookup"><span data-stu-id="2d597-350">This passage uses **Enter a path** as an example.</span></span>

    ![Visual Studio Code listesi depolama birimi yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="2d597-352">VS Code her Data Lake Analytics hesabı son ziyaret edilen yolu tutar.</span><span class="sxs-lookup"><span data-stu-id="2d597-352">VS Code keeps the last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="2d597-353">Örneğin: / tt/sn.</span><span class="sxs-lookup"><span data-stu-id="2d597-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="2d597-354">Kök yolu tarayıcısından: Seçili Data Lake Analytics hesabınızı veya yerel bir yol listesi kök yolu.</span><span class="sxs-lookup"><span data-stu-id="2d597-354">Browser from root path: The list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="2d597-355">Bir yol girin: Seçili Data Lake Analytics hesabınızı belirtilen yoldan veya yerel bir yol listesi.</span><span class="sxs-lookup"><span data-stu-id="2d597-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="2d597-356">Bir hesap, yerel yol veya bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-356">Select an account from the local path or a Data Lake Analytics account.</span></span>

    ![Visual Studio Code için Data Lake araçları depolama sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="2d597-358">Bir Azure depolama yolunu girin.</span><span class="sxs-lookup"><span data-stu-id="2d597-358">Enter an Azure storage path.</span></span> <span data-ttu-id="2d597-359">Örneğin: / çıktı.</span><span class="sxs-lookup"><span data-stu-id="2d597-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="2d597-360">Azure depolama yolunu bulun.</span><span class="sxs-lookup"><span data-stu-id="2d597-360">Find your Azure storage path.</span></span> <span data-ttu-id="2d597-361">Seçin **geçerli klasörü seç**.</span><span class="sxs-lookup"><span data-stu-id="2d597-361">Select **Choose current folder**.</span></span>

    ![Data Lake araçları Visual Studio Code için bir klasör seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="2d597-363">Sonuçları: **çıkış** penceresi dosya karşıya yükleme durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2d597-363">Results: The **Output** window displays the file upload status.</span></span>

       ![Visual Studio Code için Data Lake araçları karşıya yükleme durumu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="2d597-365">**Karşıya yüklemek için yine de ADL dosyaları: yapılandırma komutu aracılığıyla dosyasını karşıya yükle**</span><span class="sxs-lookup"><span data-stu-id="2d597-365">**To upload files though the ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="2d597-366">Komut paletini açmak veya komut dosyası Düzenleyicisi'ni sağ tıklatın ve ardından girin için Ctrl + Shift + P seçin **yapılandırma yoluyla dosyasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="2d597-366">Select Ctrl+Shift+P to open the command palette or right-click the script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="2d597-367">VS Code'da JSON dosyasını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2d597-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="2d597-368">Dosya yolları girin ve aynı anda birden çok dosya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2d597-368">You can enter file paths and upload multiple files at the same time.</span></span> <span data-ttu-id="2d597-369">Yönergeler görüntülenir **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="2d597-369">Instructions are displayed in the **Output** window.</span></span> <span data-ttu-id="2d597-370">Dosyayı karşıya yüklemeye devam etmek için (Ctrl + S) JSON dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2d597-370">To proceed to upload the file, save (Ctrl+S) the JSON file.</span></span>

       ![Visual Studio Code dosya yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="2d597-372">Sonuçları: **çıkış** penceresi dosya karşıya yükleme durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2d597-372">Results: The **Output** window displays the file upload status.</span></span>

       ![Visual Studio Code için Data Lake araçları karşıya yükleme durumu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="2d597-374">Bir dosya depolama alanına yüklemek için başka bir dosyanın tam yolunu veya dosyanın göreli yolu komut dosyası Düzenleyicisi'nde sağ tıklatma menüsünden aracılığıyla yoludur.</span><span class="sxs-lookup"><span data-stu-id="2d597-374">Another way to upload a file to storage is through the right-click menu on the file's full path or the file's relative path in the script editor.</span></span> <span data-ttu-id="2d597-375">Yerel dosya yolu girin ve sonra hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-375">Enter the local file path, and then select the account.</span></span> <span data-ttu-id="2d597-376">**Çıkış** penceresi yükleme durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2d597-376">The **Output** window displays the upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="2d597-377">Açık Azure Storage Gezgini</span><span class="sxs-lookup"><span data-stu-id="2d597-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="2d597-378">Açabilirsiniz **Azure Storage Gezgini** komutu girerek **ADL: Web Azure Storage Gezgini açmak** veya sağ tıklama bağlam menüsünden seçerek.</span><span class="sxs-lookup"><span data-stu-id="2d597-378">You can open **Azure Storage Explorer** by entering the command **ADL: Open Web Azure Storage Explorer** or by selecting it from the right-click context menu.</span></span>

<span data-ttu-id="2d597-379">**Azure Depolama Gezgini'ni açmak için**</span><span class="sxs-lookup"><span data-stu-id="2d597-379">**To open Azure Storage Explorer**</span></span>

1. <span data-ttu-id="2d597-380">Komut paletini açmak için Ctrl + Shift + P seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-380">Select Ctrl+Shift+P to open the command palette.</span></span>
2. <span data-ttu-id="2d597-381">Girin **açık Web Azure Storage Gezgini** veya göreli bir yol veya tam yolunu komut dosyası Düzenleyicisi'nde sağ tıklayın ve ardından **açık Web Azure Storage Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="2d597-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or the full path in the script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="2d597-382">Bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="2d597-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="2d597-383">Data Lake araçları Azure portalında Azure depolama yol açar.</span><span class="sxs-lookup"><span data-stu-id="2d597-383">Data Lake Tools opens the Azure storage path in the Azure portal.</span></span> <span data-ttu-id="2d597-384">FIND yol ve dosya Web'den Önizleme.</span><span class="sxs-lookup"><span data-stu-id="2d597-384">You can find the path and preview the file from the web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="2d597-385">Yerel çalıştırma ve yerel kullanıcılar için Windows hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="2d597-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="2d597-386">U-SQL yerel çalıştırma yerel verilerinizi sınar ve kodunuzu Data Lake Analytics yayımlanmadan önce komut yerel olarak doğrular.</span><span class="sxs-lookup"><span data-stu-id="2d597-386">U-SQL local run tests your local data and validates your script locally, before your code is published to Data Lake Analytics.</span></span> <span data-ttu-id="2d597-387">Yerel hata ayıklama özelliği kodunuzu Data Lake Analytics gönderilmeden önce şu görevleri tamamlamanıza sağlar:</span><span class="sxs-lookup"><span data-stu-id="2d597-387">The local debug feature enables you to complete the following tasks before your code is submitted to Data Lake Analytics:</span></span> 
- <span data-ttu-id="2d597-388">C# arka plan kod hata ayıklaması.</span><span class="sxs-lookup"><span data-stu-id="2d597-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="2d597-389">Kod üzerinden adım.</span><span class="sxs-lookup"><span data-stu-id="2d597-389">Step through the code.</span></span> 
- <span data-ttu-id="2d597-390">Komut dosyası yerel olarak doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2d597-390">Validate your script locally.</span></span>

<span data-ttu-id="2d597-391">Yerel çalıştırma ve yerel hata ayıklama hakkında yönergeler için bkz: [U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="2d597-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="2d597-392">Ek Özellikler</span><span class="sxs-lookup"><span data-stu-id="2d597-392">Additional features</span></span>

<span data-ttu-id="2d597-393">VS Code'da için Data Lake araçları aşağıdaki özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="2d597-393">Data Lake Tools for VS Code supports the following features:</span></span>

-   <span data-ttu-id="2d597-394">IntelliSense otomatik tamamlama: önerileri anahtar sözcükler, yöntemleri ve değişkenler gibi öğelerin etrafında açılır pencere görünür.</span><span class="sxs-lookup"><span data-stu-id="2d597-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="2d597-395">Farklı simgeler farklı tip nesneyi temsil eder:</span><span class="sxs-lookup"><span data-stu-id="2d597-395">Different icons represent different types of the objects:</span></span>

    - <span data-ttu-id="2d597-396">Scala veri türü</span><span class="sxs-lookup"><span data-stu-id="2d597-396">Scala data type</span></span>
    - <span data-ttu-id="2d597-397">karmaşık veri türü</span><span class="sxs-lookup"><span data-stu-id="2d597-397">Complex data type</span></span>
    - <span data-ttu-id="2d597-398">Yerleşik atama</span><span class="sxs-lookup"><span data-stu-id="2d597-398">Built-in UDTs</span></span>
    - <span data-ttu-id="2d597-399">.NET koleksiyonu ve sınıfları</span><span class="sxs-lookup"><span data-stu-id="2d597-399">.NET collection and classes</span></span>
    - <span data-ttu-id="2d597-400">C# ifadeleri</span><span class="sxs-lookup"><span data-stu-id="2d597-400">C# expressions</span></span>
    - <span data-ttu-id="2d597-401">Yerleşik C# UDF'ler, Udo'lar ve UDAAGs</span><span class="sxs-lookup"><span data-stu-id="2d597-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="2d597-402">U-SQL işlevleri</span><span class="sxs-lookup"><span data-stu-id="2d597-402">U-SQL functions</span></span>
    - <span data-ttu-id="2d597-403">U-SQL Pencereleme işlevi</span><span class="sxs-lookup"><span data-stu-id="2d597-403">U-SQL windowing function</span></span>
 
    ![Visual Studio kod IntelliSense nesne türleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="2d597-405">IntelliSense otomatik tamamlama Data Lake Analytics meta: Data Lake araçları, Data Lake Analytics meta veri bilgileri yerel olarak indirir.</span><span class="sxs-lookup"><span data-stu-id="2d597-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads the Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="2d597-406">IntelliSense özelliği, veritabanı, şema, tablo, görünüm, tablo değerli işlevi, yordamlar ve C# derlemeleri, Data Lake Analytics meta veriler dahil olmak üzere nesneleri, otomatik olarak doldurur.</span><span class="sxs-lookup"><span data-stu-id="2d597-406">The IntelliSense feature automatically populates objects, including the database, schema, table, view, table-valued function, procedures, and C# assemblies, from the Data Lake Analytics metadata.</span></span>
 
    ![Visual Studio kod IntelliSense meta verileri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="2d597-408">IntelliSense hata işaret: Data Lake araçları U-SQL ve C# için düzenleme hataları altını çizer.</span><span class="sxs-lookup"><span data-stu-id="2d597-408">IntelliSense error marker: Data Lake Tools underlines the editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="2d597-409">Sözdizimi vurgular: Data Lake araçları, değişkenleri, anahtar sözcükler, veri türü ve işlevleri gibi öğeleri ayırt etmek için farklı bir renk kullanır.</span><span class="sxs-lookup"><span data-stu-id="2d597-409">Syntax highlights: Data Lake Tools uses different colors to differentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Visual Studio Code sözdizimi için Data Lake araçları vurgular](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="2d597-411">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2d597-411">Next steps</span></span>

- <span data-ttu-id="2d597-412">U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama için bkz: [U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="2d597-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="2d597-413">Başlama Data Lake Analytics hakkında bilgi için bkz: [Öğreticisi: Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2d597-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="2d597-414">Visual Studio için Data Lake araçları hakkında bilgi için bkz: [öğretici: Visual Studio için Data Lake araçları kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2d597-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="2d597-415">Derlemeler geliştirme hakkında daha fazla bilgi için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="2d597-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



