---
title: "Azure Data Lake araçları: Kullanım Azure Data Lake araçları Visual Studio kodunu | Microsoft Docs"
description: "Nasıl toouse Azure Data Lake araçları Visual Studio Code toocreate için test ve U-SQL betikleri çalıştırmak öğrenin. "
Keywords: "VScode, Azure Data Lake araçları, yerel çalıştırma, yerel hata ayıklama, yerel hata ayıklama, Önizleme depolama dosyası toostorage yolu karşıya yükle"
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
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a><span data-ttu-id="5ca3c-104">Azure Data Lake araçları Visual Studio kodunu kullanın</span><span class="sxs-lookup"><span data-stu-id="5ca3c-104">Use Azure Data Lake Tools for Visual Studio Code</span></span>

<span data-ttu-id="5ca3c-105">Nasıl toouse Azure Data Lake araçları Visual Studio Code (VS Code) toocreate için test ve U-SQL betikleri çalıştırmak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-105">Learn how toouse Azure Data Lake Tools for Visual Studio Code (VS Code) toocreate, test, and run U-SQL scripts.</span></span> <span data-ttu-id="5ca3c-106">Merhaba bilgileri de video aşağıdaki hello ele alınmıştır:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-106">hello information is also covered in hello following video:</span></span>

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a><span data-ttu-id="5ca3c-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5ca3c-107">Prerequisites</span></span>

<span data-ttu-id="5ca3c-108">Data Lake araçları, VS kodu tarafından desteklenen hello platformlarda yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-108">Data Lake Tools can be installed on hello platforms supported by VS Code.</span></span> <span data-ttu-id="5ca3c-109">Merhaba desteklenen platformlar, Windows, Linux ve MacOS içerir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-109">hello supported platforms include Windows, Linux, and MacOS.</span></span> <span data-ttu-id="5ca3c-110">Hello farklı platformlarda hello aşağıdaki önkoşullar vardır:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-110">hello different platforms have hello following prerequisites:</span></span>

- <span data-ttu-id="5ca3c-111">Windows</span><span class="sxs-lookup"><span data-stu-id="5ca3c-111">Windows</span></span>

    - <span data-ttu-id="5ca3c-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-112">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="5ca3c-113">[Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-113">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="5ca3c-114">Merhaba java.exe yol toohello sistem ortam değişkeni yol ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-114">Add hello java.exe path toohello system environment variable path.</span></span> <span data-ttu-id="5ca3c-115">Yapılandırma yönergeleri için bkz: [nasıl ayarlayın veya hello Path sistem değişkeni değiştirme?]( https://www.java.com/download/help/path.xml).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-115">For configuration instructions, see [How do I set or change hello Path system variable?]( https://www.java.com/download/help/path.xml).</span></span> <span data-ttu-id="5ca3c-116">Merhaba, benzer tooC:\Program Files\Java\jdk1.8.0_77\jre\bin yoludur.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-116">hello path is similar tooC:\Program Files\Java\jdk1.8.0_77\jre\bin.</span></span>
    - <span data-ttu-id="5ca3c-117">[.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-117">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
    
- <span data-ttu-id="5ca3c-118">Linux (Ubuntu 14.04 LTS önerilir)</span><span class="sxs-lookup"><span data-stu-id="5ca3c-118">Linux (We recommend Ubuntu 14.04 LTS)</span></span>

    - <span data-ttu-id="5ca3c-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-119">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span> <span data-ttu-id="5ca3c-120">tooinstall Merhaba kod, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-120">tooinstall hello code, enter hello following command:</span></span>

              sudo dpkg -i code_<version_number>_amd64.deb

    - <span data-ttu-id="5ca3c-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-121">[Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/).</span></span> 

        - <span data-ttu-id="5ca3c-122">tooupdate hello deb paket kaynağı, hello aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-122">tooupdate hello deb package source, enter hello following commands:</span></span>

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - <span data-ttu-id="5ca3c-123">tooinstall Mono, komutu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-123">tooinstall Mono, enter hello following command:</span></span>

                sudo apt-get install mono-complete

            > [!NOTE] 
            > <span data-ttu-id="5ca3c-124">Mono 4.6 desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-124">Mono 4.6 is not supported.</span></span> <span data-ttu-id="5ca3c-125">Tamamen 4.2.x yüklemeden önce sürüm 4.6 kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-125">Uninstall version 4.6 entirely before you install 4.2.x.</span></span>  

        - <span data-ttu-id="5ca3c-126">[Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-126">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="5ca3c-127">Yükleme yönergeleri için bkz: Merhaba [Linux 64 bit yükleme yönergeleri için Java]( https://java.com/en/download/help/linux_x64_install.xml) sayfası.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-127">For instructions on installation, see hello [Linux 64-bit installation instructions for Java]( https://java.com/en/download/help/linux_x64_install.xml) page.</span></span>
        - <span data-ttu-id="5ca3c-128">[.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-128">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>
- <span data-ttu-id="5ca3c-129">macOS</span><span class="sxs-lookup"><span data-stu-id="5ca3c-129">MacOS</span></span>

    - <span data-ttu-id="5ca3c-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-130">[Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).</span></span>
    - <span data-ttu-id="5ca3c-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-131">[Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/).</span></span> 
    - <span data-ttu-id="5ca3c-132">[Java SE çalışma zamanı ortamı sürüm 8 güncelleştirme 77 veya sonrası](https://java.com/download/manual.jsp).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-132">[Java SE Runtime Environment version 8 update 77 or later](https://java.com/download/manual.jsp).</span></span> <span data-ttu-id="5ca3c-133">Yükleme yönergeleri için bkz: Merhaba [Linux 64 bit yükleme yönergeleri için Java](https://java.com/en/download/help/mac_install.xml) sayfası.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-133">For instructions on installation, see hello [Linux 64-bit installation instructions for Java](https://java.com/en/download/help/mac_install.xml) page.</span></span>
    - <span data-ttu-id="5ca3c-134">[.NET core SDK 1.0.3 veya .NET Core 1.1 çalışma zamanı](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-134">[.NET Core SDK 1.0.3 or .NET Core 1.1 runtime](https://www.microsoft.com/net/download).</span></span>

## <a name="install-data-lake-tools"></a><span data-ttu-id="5ca3c-135">Data Lake araçları yükleme</span><span class="sxs-lookup"><span data-stu-id="5ca3c-135">Install Data Lake Tools</span></span>

<span data-ttu-id="5ca3c-136">Merhaba önkoşulları yüklendikten sonra VS Code için Data Lake araçları yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-136">After you install hello prerequisites, you can install Data Lake Tools for VS Code.</span></span>

<span data-ttu-id="5ca3c-137">**tooinstall Data Lake araçları**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-137">**tooinstall Data Lake Tools**</span></span>

1. <span data-ttu-id="5ca3c-138">Visual Studio Code'da açın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-138">Open Visual Studio Code.</span></span>
2. <span data-ttu-id="5ca3c-139">CTRL + P seçin ve ardından hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-139">Select Ctrl+P, and then enter hello following command:</span></span>
```
ext install usql-vscode-ext
```
<span data-ttu-id="5ca3c-140">Visual Studio kod uzantılarının bir listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-140">You can see a list of Visual Studio code extensions.</span></span> <span data-ttu-id="5ca3c-141">Bunlardan biri olan **Azure Data Lake Araçları**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-141">One of them is **Azure Data Lake Tools**.</span></span>

3. <span data-ttu-id="5ca3c-142">Seçin **yükleme** sonraki çok**Azure Data Lake Araçları**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-142">Select **Install** next too**Azure Data Lake Tools**.</span></span> <span data-ttu-id="5ca3c-143">Birkaç saniye sonra hello **yükleme** düğmesini değişiklikleri çok**yeniden**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-143">After a few seconds, hello **Install** button changes too**Reload**.</span></span>
4. <span data-ttu-id="5ca3c-144">Seçin **yeniden** tooactivate hello uzantısı.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-144">Select **Reload** tooactivate hello extension.</span></span>
5. <span data-ttu-id="5ca3c-145">Seçin **Tamam** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-145">Select **OK** tooconfirm.</span></span> <span data-ttu-id="5ca3c-146">Azure Data Lake araçları hello görebilirsiniz **uzantıları** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-146">You can see Azure Data Lake Tools in hello **Extensions** pane.</span></span>
    <span data-ttu-id="5ca3c-147">![Visual Studio kod uzantılarını bölmesi için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span><span class="sxs-lookup"><span data-stu-id="5ca3c-147">![Data Lake Tools for Visual Studio Code Extensions pane](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)</span></span>

## <a name="activate-azure-data-lake-tools"></a><span data-ttu-id="5ca3c-148">Azure Data Lake araçları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5ca3c-148">Activate Azure Data Lake Tools</span></span>
<span data-ttu-id="5ca3c-149">Yeni bir .usql dosyası oluşturun veya varolan .usql dosya tooactivate hello uzantı açın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-149">Create a new .usql file or open an existing .usql file tooactivate hello extension.</span></span> 

## <a name="connect-tooazure"></a><span data-ttu-id="5ca3c-150">TooAzure Bağlan</span><span class="sxs-lookup"><span data-stu-id="5ca3c-150">Connect tooAzure</span></span>

<span data-ttu-id="5ca3c-151">Derleme ve Data Lake Analytics U-SQL betikleri çalıştırmak için önce tooyour Azure hesabı bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-151">Before you can compile and run U-SQL scripts in Data Lake Analytics, you must connect tooyour Azure account.</span></span>

<span data-ttu-id="5ca3c-152">**tooconnect tooAzure**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-152">**tooconnect tooAzure**</span></span>

1.  <span data-ttu-id="5ca3c-153">Ctrl + Shift + P tooopen hello komutu palet seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-153">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2.  <span data-ttu-id="5ca3c-154">Girin **ADL: oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-154">Enter **ADL: Login**.</span></span> <span data-ttu-id="5ca3c-155">Merhaba oturum açma bilgilerini görünür hello **çıkış** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-155">hello login information appears in hello **Output** pane.</span></span>

    <span data-ttu-id="5ca3c-156">![Data Lake araçları Visual Studio Code komutu paletini](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Visual Studio Code cihaz oturum açma bilgileri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span><span class="sxs-lookup"><span data-stu-id="5ca3c-156">![Data Lake Tools for Visual Studio Code command palette](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
![Data Lake Tools for Visual Studio Code device login information](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)</span></span>
3. <span data-ttu-id="5ca3c-157">Seçin CTRL + hello oturum açma URL'ı tıklatın: https://aka.ms/devicelogin tooopen hello oturum açma Web sayfası.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-157">Select Ctrl+click on hello login URL: https://aka.ms/devicelogin tooopen hello login webpage.</span></span> <span data-ttu-id="5ca3c-158">Merhaba kodu girin **G567LX42V** hello metin kutusuna ve ardından **devam**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-158">Enter hello code **G567LX42V** into hello text box, and then select **Continue**.</span></span>

   ![Visual Studio Code oturum açma için Data Lake araçları kodu yapıştırın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  <span data-ttu-id="5ca3c-160">Merhaba yönergeleri toosign hello Web sayfasından izleyin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-160">Follow hello instructions toosign in from hello webpage.</span></span> <span data-ttu-id="5ca3c-161">Bağlandığınızda, Azure hesap adınızı hello durum çubuğunda hello sol alt köşesinde hello görüntülenir. **VS Code** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-161">When you're connected, your Azure account name appears on hello status bar in hello lower-left corner of hello **VS Code** window.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="5ca3c-162">İki etmen etkin hesabınız varsa, PIN kullanmak yerine telefon kimlik doğrulaması kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-162">If your account has two factors enabled, we recommend that you use phone authentication rather than using a PIN.</span></span>

<span data-ttu-id="5ca3c-163">Çıkış toosign hello komutu girin **ADL: oturum kapatma**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-163">toosign out, enter hello command **ADL: Logout**.</span></span>

## <a name="list-your-data-lake-analytics-accounts"></a><span data-ttu-id="5ca3c-164">Data Lake Analytics hesaplarını listeler</span><span class="sxs-lookup"><span data-stu-id="5ca3c-164">List your Data Lake Analytics accounts</span></span>

<span data-ttu-id="5ca3c-165">tootest hello bağlantısı, bir Data Lake Analytics hesapları listesini alın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-165">tootest hello connection, get a list of your Data Lake Analytics accounts.</span></span>

<span data-ttu-id="5ca3c-166">**Azure aboneliğinizdeki toolist hello Data Lake Analytics hesapları**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-166">**toolist hello Data Lake Analytics accounts under your Azure subscription**</span></span>

1. <span data-ttu-id="5ca3c-167">Ctrl + Shift + P tooopen hello komutu palet seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-167">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="5ca3c-168">Girin **ADL: liste hesapları**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-168">Enter **ADL: List Accounts**.</span></span> <span data-ttu-id="5ca3c-169">Merhaba hesapları görünmez hello **çıkış** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-169">hello accounts appear in hello **Output** pane.</span></span>

## <a name="open-hello-sample-script"></a><span data-ttu-id="5ca3c-170">Açık hello örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="5ca3c-170">Open hello sample script</span></span>
<span data-ttu-id="5ca3c-171">Merhaba komutu palet (Ctrl + Shift + P) açın ve girin **ADL: açık örnek komut dosyası**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-171">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Open Sample Script**.</span></span> <span data-ttu-id="5ca3c-172">Bu örnek başka bir örneği açılır.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-172">This opens another instance of this sample.</span></span> <span data-ttu-id="5ca3c-173">Ayrıca düzenleyebilir, yapılandırmak ve bu örnek komut gönderme.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-173">You can also edit, configure, and submit script on this instance.</span></span>

## <a name="work-with-u-sql"></a><span data-ttu-id="5ca3c-174">U-SQL ile çalışma</span><span class="sxs-lookup"><span data-stu-id="5ca3c-174">Work with U-SQL</span></span>

<span data-ttu-id="5ca3c-175">U-SQL ile bir U-SQL dosya veya klasör toowork açın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-175">You need open either a U-SQL file or a folder toowork with U-SQL.</span></span>

<span data-ttu-id="5ca3c-176">**U-SQL projeniz için bir klasör tooopen**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-176">**tooopen a folder for your U-SQL project**</span></span>

1. <span data-ttu-id="5ca3c-177">Visual Studio koddan hello seçin **dosya** menüsüne ve ardından **Klasör Aç**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-177">From Visual Studio Code, select hello **File** menu, and then select **Open Folder**.</span></span>
2. <span data-ttu-id="5ca3c-178">Bir klasör belirtin ve ardından **Klasör Seç**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-178">Specify a folder, and then select **Select Folder**.</span></span>
3. <span data-ttu-id="5ca3c-179">Select hello **dosya** menüsüne ve ardından **yeni**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-179">Select hello **File** menu, and then select **New**.</span></span> <span data-ttu-id="5ca3c-180">Adsız-1 dosya toohello projesi eklenir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-180">An Untitled-1 file is added toohello project.</span></span>
4. <span data-ttu-id="5ca3c-181">Merhaba adsız 1 dosyasına koddan hello girin:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-181">Enter hello following code into hello Untitled-1 file:</span></span>

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

    <span data-ttu-id="5ca3c-182">Merhaba betik hello/Output klasöründe bulunan bazı veriler içeren bir departments.csv dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-182">hello script creates a departments.csv file with some data included in hello /output folder.</span></span>

5. <span data-ttu-id="5ca3c-183">Merhaba dosyası olarak kaydetmeniz **myUSQL.usql** hello klasörünü açılır.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-183">Save hello file as **myUSQL.usql** in hello opened folder.</span></span> <span data-ttu-id="5ca3c-184">Bir adltools_settings.json yapılandırma dosyası da toohello projesi eklenir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-184">A adltools_settings.json configuration file is also added toohello project.</span></span>
4. <span data-ttu-id="5ca3c-185">Açın ve aşağıdaki özelliklere hello ile adltools_settings.json yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-185">Open and configure adltools_settings.json with hello following properties:</span></span>

    - <span data-ttu-id="5ca3c-186">: Bir Data Lake Analytics hesabı, Azure aboneliğinizin altında.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-186">Account:  A Data Lake Analytics account under your Azure subscription.</span></span>
    - <span data-ttu-id="5ca3c-187">Veritabanı: Hesabınız altındaki bir veritabanı.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-187">Database: A database under your account.</span></span> <span data-ttu-id="5ca3c-188">Merhaba varsayılandır **ana**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-188">hello default is **master**.</span></span>
    - <span data-ttu-id="5ca3c-189">Şema: Veritabanınızı altında bir şema.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-189">Schema: A schema under your database.</span></span> <span data-ttu-id="5ca3c-190">Merhaba varsayılandır **dbo**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-190">hello default is **dbo**.</span></span>
    - <span data-ttu-id="5ca3c-191">İsteğe bağlı ayarlar:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-191">Optional settings:</span></span>
        - <span data-ttu-id="5ca3c-192">Öncelik: hello öncelik aralığı 1 ile 1 too1000 hello en yüksek öncelikli olarak arasındadır.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-192">Priority: hello priority range is from 1 too1000 with 1 as hello highest priority.</span></span> <span data-ttu-id="5ca3c-193">Merhaba varsayılan değer **1000**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-193">hello default value is **1000**.</span></span>
        - <span data-ttu-id="5ca3c-194">Paralellik: 1 too150 hello paralellik aralıktır.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-194">Parallelism: hello parallelism range is from 1 too150.</span></span> <span data-ttu-id="5ca3c-195">Azure Data Lake Analytics hesabınızı izin verilen maksimum paralellik hello Hello varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-195">hello default value is hello maximum parallelism allowed in your Azure Data Lake Analytics account.</span></span> 
        
        > [!NOTE] 
        > <span data-ttu-id="5ca3c-196">Hello ayarları geçersiz varsa, hello varsayılan değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-196">If hello settings are invalid, hello default values are used.</span></span>

    ![Visual Studio Code yapılandırma dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    <span data-ttu-id="5ca3c-198">Data Lake Analytics hesabı bir işlem toocompile ve Çalıştır U-SQL işleri gerekli.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-198">A compute Data Lake Analytics account is needed toocompile and run U-SQL jobs.</span></span> <span data-ttu-id="5ca3c-199">Derleme ve U-SQL işleri çalıştırma önce hello bilgisayar hesabı yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-199">You must configure hello computer account before you can compile and run U-SQL jobs.</span></span>
    
<span data-ttu-id="5ca3c-200">Merhaba yapılandırma kaydedildikten sonra hello hesap, veritabanı ve şema bilgilerini hello sol alt köşesindeki hello karşılık gelen .usql dosyası hello durum çubuğunda görünür.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-200">After hello configuration is saved, hello account, database, and schema information appears on hello status bar at hello bottom-left corner of hello corresponding .usql file.</span></span> 
 
 
<span data-ttu-id="5ca3c-201">Karşılaştırılan tooopening yapabileceğiniz bir klasörü açtığınızda, bir dosya:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-201">Compared tooopening a file, when you open a folder you can:</span></span>

- <span data-ttu-id="5ca3c-202">Arka plan kodu dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-202">Use a code-behind file.</span></span> <span data-ttu-id="5ca3c-203">Arka plan kodu Hello tek dosya modunda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-203">In hello single-file mode, code-behind is not supported.</span></span>
- <span data-ttu-id="5ca3c-204">Bir yapılandırma dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-204">Use a configuration file.</span></span> <span data-ttu-id="5ca3c-205">Bir klasörü açtığınızda, çalışma klasörü hello hello betiklerde tek yapılandırma dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-205">When you open a folder, hello scripts in hello working folder share a single configuration file.</span></span>


<span data-ttu-id="5ca3c-206">U-SQL betiği Hello hello Data Lake Analytics hizmeti uzaktan derler.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-206">hello U-SQL script compiles remotely through hello Data Lake Analytics service.</span></span> <span data-ttu-id="5ca3c-207">Merhaba çıkarırsanız **derleme** komutunu hello U-SQL betiği tooyour Data Lake Analytics hesabı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-207">When you issue hello **compile** command, hello U-SQL script is sent tooyour Data Lake Analytics account.</span></span> <span data-ttu-id="5ca3c-208">Daha sonra Visual Studio Code hello derleme sonucu alır.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-208">Later, Visual Studio Code receives hello compilation result.</span></span> <span data-ttu-id="5ca3c-209">Toohello uzak derleme, Visual Studio Code tooconnect tooyour hello yapılandırma dosyasında Data Lake Analytics hesabı hello bilgileri listelemek gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-209">Due toohello remote compilation, Visual Studio Code requires that you list hello information tooconnect tooyour Data Lake Analytics account in hello configuration file.</span></span>

<span data-ttu-id="5ca3c-210">**toocompile U-SQL komut dosyası**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-210">**toocompile a U-SQL script**</span></span>

1. <span data-ttu-id="5ca3c-211">Ctrl + Shift + P tooopen hello komutu palet seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-211">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="5ca3c-212">Girin **ADL: derleme betik**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-212">Enter **ADL: Compile Script**.</span></span> <span data-ttu-id="5ca3c-213">Merhaba derleme sonuçları görünen hello **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-213">hello compile results appear in hello **Output** window.</span></span> <span data-ttu-id="5ca3c-214">Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: derleme betik** toocompile U-SQL işi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-214">You can also right-click a script file, and then select **ADL: Compile Script** toocompile a U-SQL job.</span></span> <span data-ttu-id="5ca3c-215">Merhaba derleme sonucu görünür hello **çıkış** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-215">hello compilation result appears in hello **Output** pane.</span></span>
 

<span data-ttu-id="5ca3c-216">**toosubmit U-SQL komut dosyası**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-216">**toosubmit a U-SQL script**</span></span>

1. <span data-ttu-id="5ca3c-217">Ctrl + Shift + P tooopen hello komutu palet seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-217">Select Ctrl+Shift+P tooopen hello command palette.</span></span> 
2. <span data-ttu-id="5ca3c-218">Girin **ADL: işi göndermek**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-218">Enter **ADL: Submit Job**.</span></span>  <span data-ttu-id="5ca3c-219">Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: işi Gönder**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-219">You can also right-click a script file, and then select **ADL: Submit Job**.</span></span> 

<span data-ttu-id="5ca3c-220">U-SQL işi gönderdikten sonra hello gönderimi günlükleri hello görünür **çıkış** VS Code penceresinde.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-220">After you submit a U-SQL job, hello submission logs appear in hello **Output** window in VS Code.</span></span> <span data-ttu-id="5ca3c-221">Merhaba gönderme başarılı olursa, hello iş URL de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-221">If hello submission is successful, hello job URL appears as well.</span></span> <span data-ttu-id="5ca3c-222">Bir web tarayıcısı tootrack hello gerçek zamanlı iş durumu hello iş URL açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-222">You can open hello job URL in a web browser tootrack hello real-time job status.</span></span>

<span data-ttu-id="5ca3c-223">Merhaba iş ayrıntıları, tooenable hello çıktısı ayarlamak **jobInformationOutputPath** hello içinde **vs code hello u-sql_settings.json için** dosya.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-223">tooenable hello output of hello job details, set **jobInformationOutputPath** in hello **vs code for hello u-sql_settings.json** file.</span></span>
 
## <a name="use-a-code-behind-file"></a><span data-ttu-id="5ca3c-224">Bir arka plan kod dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="5ca3c-224">Use a code-behind file</span></span>

<span data-ttu-id="5ca3c-225">Tek bir U-SQL betiği ile ilişkili bir C# dosyasına bir arka plan kodu dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-225">A code-behind file is a C# file associated with a single U-SQL script.</span></span> <span data-ttu-id="5ca3c-226">Ayrılmış betik tooUDO, UDA, UDT ve UDF hello arka plan kod dosyasına tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-226">You can define a script dedicated tooUDO, UDA, UDT, and UDF in hello code-behind file.</span></span> <span data-ttu-id="5ca3c-227">Merhaba UDO, UDA, UDT ve UDF doğrudan hello komut dosyasında hello derleme ilk kaydettirmeden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-227">hello UDO, UDA, UDT, and UDF can be used directly in hello script without registering hello assembly first.</span></span> <span data-ttu-id="5ca3c-228">Merhaba arka plan kod dosyasına hello aynı yerleştirileceği klasörü kendi eşleme U-SQL komut dosyası olarak.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-228">hello code-behind file is put in hello same folder as its peering U-SQL script file.</span></span> <span data-ttu-id="5ca3c-229">Merhaba betik xxx.usql olarak adlandırılmışsa hello arka plan kod xxx.usql.cs adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-229">If hello script is named xxx.usql, hello code-behind is named as xxx.usql.cs.</span></span> <span data-ttu-id="5ca3c-230">Merhaba arka plan kodu dosyasını el ile silin, hello arka plan kodu özelliği, ilişkili U-SQL betiği için devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-230">If you manually delete hello code-behind file, hello code-behind feature is disabled for its associated U-SQL script.</span></span> <span data-ttu-id="5ca3c-231">U-SQL betiği için müşteri kod yazma hakkında daha fazla bilgi için bkz: [yazma ve özel kodda kullanarak U-SQL: kullanıcı tanımlı işlevler]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-231">For more information about writing customer code for U-SQL script, see [Writing and Using Custom Code in U-SQL: User-Defined Functions]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).</span></span>

<span data-ttu-id="5ca3c-232">toosupport arka plan kod, bir çalışma klasörü açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-232">toosupport code-behind, you must open a working folder.</span></span> 

<span data-ttu-id="5ca3c-233">**toogenerate bir arka plan kod dosyası**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-233">**toogenerate a code-behind file**</span></span>

1. <span data-ttu-id="5ca3c-234">Bir kaynak dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-234">Open a source file.</span></span> 
2. <span data-ttu-id="5ca3c-235">Ctrl + Shift + P tooopen hello komutu palet seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-235">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
3. <span data-ttu-id="5ca3c-236">Girin **ADL: arka plan kod oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-236">Enter **ADL: Generate Code Behind**.</span></span> <span data-ttu-id="5ca3c-237">Bir arka plan kod dosyası hello aynı oluşturulur klasör.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-237">A code-behind file is created in hello same folder.</span></span> 

<span data-ttu-id="5ca3c-238">Ayrıca bir komut dosyasını sağ tıklatın ve ardından **ADL: kod arkasında oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-238">You can also right-click a script file, and then select **ADL: Generate Code Behind**.</span></span> 

<span data-ttu-id="5ca3c-239">toocompile ve U-SQL betiği bir arka plan kod dosyası ile aynı hello tek başına U-SQL ile dosyası hello olduğu gönderin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-239">toocompile and submit a U-SQL script with a code-behind file is hello same as with hello standalone U-SQL script file.</span></span>

<span data-ttu-id="5ca3c-240">iki ekran görüntüleri aşağıdaki hello bir arka plan kod dosyası ve onun ilişkili U-SQL komut dosyası gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-240">hello following two screenshots show a code-behind file and its associated U-SQL script file:</span></span>
 
![Visual Studio Code arka plan kod için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Visual Studio Code arka plan kodu komut dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a><span data-ttu-id="5ca3c-243">Derlemeleri kullanma</span><span class="sxs-lookup"><span data-stu-id="5ca3c-243">Use assemblies</span></span>

<span data-ttu-id="5ca3c-244">Derlemeler geliştirme hakkında daha fazla bilgi için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-244">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>

<span data-ttu-id="5ca3c-245">Data Lake araçları tooregister özel kod derlemeleri hello Data Lake Analytics Kataloğu'nda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-245">You can use Data Lake Tools tooregister custom code assemblies in hello Data Lake Analytics catalog.</span></span>

<span data-ttu-id="5ca3c-246">**tooregister derleme**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-246">**tooregister an assembly**</span></span>

<span data-ttu-id="5ca3c-247">Merhaba derleme hello aracılığıyla kaydedebilirsiniz **ADL: kaydetmek derleme** veya **ADL: kaydetmek derleme yapılandırma yoluyla** komutları.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-247">You can register hello assembly through hello **ADL: Register Assembly** or **ADL: Register Assembly through Configuration** commands.</span></span>

<span data-ttu-id="5ca3c-248">**Merhaba ADL aracılığıyla tooregister: kaydetmek derleme komutu**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-248">**tooregister through hello ADL: Register Assembly command**</span></span>
1.  <span data-ttu-id="5ca3c-249">Ctrl + Shift + P tooopen hello komutu palet seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-249">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="5ca3c-250">Girin **ADL: kaydetmek derleme**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-250">Enter **ADL: Register Assembly**.</span></span> 
3.  <span data-ttu-id="5ca3c-251">Merhaba yerel derleme yolu belirtin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-251">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="5ca3c-252">Bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-252">Select a Data Lake Analytics account.</span></span>
5.  <span data-ttu-id="5ca3c-253">Bir veritabanı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-253">Select a database.</span></span>

<span data-ttu-id="5ca3c-254">Sonuçları: hello portalı bir tarayıcıda açıldığından ve hello derleme kayıt işlemi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-254">Results: hello portal is opened in a browser and displays hello assembly registration process.</span></span>  

<span data-ttu-id="5ca3c-255">Başka bir uygun şekilde tootrigger hello **ADL: kaydetmek derleme** tooright tıklatma hello .dll dosyasının dosya Gezgini'nde bir komuttur.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-255">Another convenient way tootrigger hello **ADL: Register Assembly** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="5ca3c-256">**tooregister ancak hello ADL: kaydetmek derleme yapılandırma komutu**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-256">**tooregister though hello ADL: Register Assembly through Configuration command**</span></span>
1.  <span data-ttu-id="5ca3c-257">Ctrl + Shift + P tooopen hello komutu palet seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-257">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2.  <span data-ttu-id="5ca3c-258">Girin **ADL: kaydetmek derleme yapılandırma yoluyla**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-258">Enter **ADL: Register Assembly through Configuration**.</span></span> 
3.  <span data-ttu-id="5ca3c-259">Merhaba yerel derleme yolu belirtin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-259">Specify hello local assembly path.</span></span> 
4.  <span data-ttu-id="5ca3c-260">Merhaba JSON dosyası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-260">hello JSON file is displayed.</span></span> <span data-ttu-id="5ca3c-261">Gözden geçirin ve gerekirse hello derleme bağımlılıkları ve kaynak parametreleri düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-261">Review and edit hello assembly dependencies and resource parameters, if needed.</span></span> <span data-ttu-id="5ca3c-262">Yönergeler hello görüntülenen **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-262">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="5ca3c-263">tooproceed toohello derleme kaydı (Ctrl + S) hello JSON dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-263">tooproceed toohello assembly registration, save (Ctrl+S) hello JSON file.</span></span>

![Visual Studio Code arka plan kod için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- <span data-ttu-id="5ca3c-265">Derleme bağımlılıkları: Azure Data Lake araçları autodetects hello DLL bağımlılıkları sahip olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-265">Assembly dependencies: Azure Data Lake Tools autodetects whether hello DLL has any dependencies.</span></span> <span data-ttu-id="5ca3c-266">algılandıkları sonra hello bağımlılıkları hello JSON dosyasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-266">hello dependencies are displayed in hello JSON file after they are detected.</span></span> 
>- <span data-ttu-id="5ca3c-267">Kaynaklar: Hello derleme kaydı bir parçası olarak, DLL kaynakları (örneğin, .txt, .png ve .csv) karşıya yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-267">Resources: You can upload your DLL resources (for example, .txt, .png, and .csv) as part of hello assembly registration.</span></span> 

<span data-ttu-id="5ca3c-268">Başka bir şekilde tootrigger hello **ADL: kaydetmek derleme yapılandırma yoluyla** tooright tıklatma hello .dll dosyasının dosya Gezgini'nde bir komuttur.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-268">Another way tootrigger hello **ADL: Register Assembly through Configuration** command is tooright-click hello .dll file in File Explorer.</span></span> 

<span data-ttu-id="5ca3c-269">U-SQL kodunu aşağıdaki hello gösteren nasıl toocall derleme.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-269">hello following U-SQL code demonstrates how toocall an assembly.</span></span> <span data-ttu-id="5ca3c-270">Merhaba örnek hello derleme adı: *test*.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-270">In hello sample, hello assembly name is *test*.</span></span>

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
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a><span data-ttu-id="5ca3c-271">Merhaba Data Lake Analytics Kataloğu'na erişme</span><span class="sxs-lookup"><span data-stu-id="5ca3c-271">Access hello Data Lake Analytics catalog</span></span>

<span data-ttu-id="5ca3c-272">TooAzure bağlandıktan sonra aşağıdaki adımları tooaccess hello U-SQL kataloğunu hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-272">After you have connected tooAzure, you can use hello following steps tooaccess hello U-SQL catalog.</span></span>

<span data-ttu-id="5ca3c-273">**tooaccess hello Azure Data Lake Analytics meta verileri**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-273">**tooaccess hello Azure Data Lake Analytics metadata**</span></span>

1.  <span data-ttu-id="5ca3c-274">Ctrl + Shift + P seçin ve ardından girin **ADL: liste tabloları**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-274">Select Ctrl+Shift+P, and then enter **ADL: List Tables**.</span></span>
2.  <span data-ttu-id="5ca3c-275">Merhaba Data Lake Analytics hesaplardan birini seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-275">Select one of hello Data Lake Analytics accounts.</span></span>
3.  <span data-ttu-id="5ca3c-276">Merhaba Data Lake Analytics veritabanlarından birini seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-276">Select one of hello Data Lake Analytics databases.</span></span>
4.  <span data-ttu-id="5ca3c-277">Merhaba şemaları birini seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-277">Select one of hello schemas.</span></span> <span data-ttu-id="5ca3c-278">Tabloları hello listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-278">You can see hello list of tables.</span></span>

## <a name="view-data-lake-analytics-jobs"></a><span data-ttu-id="5ca3c-279">Görünüm Data Lake Analytics işleri</span><span class="sxs-lookup"><span data-stu-id="5ca3c-279">View Data Lake Analytics jobs</span></span>

<span data-ttu-id="5ca3c-280">**tooview Data Lake Analytics işleri**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-280">**tooview Data Lake Analytics jobs**</span></span>
1.  <span data-ttu-id="5ca3c-281">Merhaba komutu palet (Ctrl + Shift + P) açıp seçin **ADL: Göster iş**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-281">Open hello command palette (Ctrl+Shift+P) and select **ADL: Show Job**.</span></span> 
2.  <span data-ttu-id="5ca3c-282">Bir Data Lake Analytics veya yerel bir hesap seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-282">Select a Data Lake Analytics or local account.</span></span> 
3.  <span data-ttu-id="5ca3c-283">Merhaba işleri listesini hello hesap tooappear için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-283">Wait for hello jobs list for hello account tooappear.</span></span>
4.  <span data-ttu-id="5ca3c-284">İş listesinden bir iş seçin, Data Lake araçları hello Azure portal hello iş ayrıntılarını açar ve VS Code'da hello iş tanımı dosyası gösterir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-284">Select a job from job list, Data Lake Tools opens hello job details in hello Azure portal and displays hello JobInfo file in VS Code.</span></span>

![Visual Studio kod IntelliSense nesne türleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a><span data-ttu-id="5ca3c-286">Azure Data Lake Storage tümleştirme</span><span class="sxs-lookup"><span data-stu-id="5ca3c-286">Azure Data Lake Storage integration</span></span>

<span data-ttu-id="5ca3c-287">Azure Data Lake Store ile ilgili komutları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-287">You can use Azure Data Lake Storage-related commands to:</span></span>
 - <span data-ttu-id="5ca3c-288">Üzerinden Hello Azure Data Lake Storage kaynaklara göz atın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-288">Browse through hello Azure Data Lake Storage resources.</span></span> 
 - <span data-ttu-id="5ca3c-289">Önizleme hello Azure Data Lake Storage dosyası.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-289">Preview hello Azure Data Lake Storage file.</span></span>  
 - <span data-ttu-id="5ca3c-290">Merhaba karşıya tooAzure Data Lake Storage VS Code'da dosyasını doğrudan.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-290">Upload hello file directly tooAzure Data Lake Storage in VS Code.</span></span> 

### <a name="list-hello-storage-path"></a><span data-ttu-id="5ca3c-291">Liste hello depolama yolu</span><span class="sxs-lookup"><span data-stu-id="5ca3c-291">List hello storage path</span></span> 
<span data-ttu-id="5ca3c-292">Merhaba depolama yolu hello komutu palet ya da sağ tıklatma listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-292">You can list hello storage path through hello command palette or through right-click.</span></span>

<span data-ttu-id="5ca3c-293">**Merhaba komutu palet üzerinden toolist hello depolama yolu**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-293">**toolist hello storage path through hello command palette**</span></span>

1.  <span data-ttu-id="5ca3c-294">Merhaba komutu palet (Ctrl + Shift + P) açın ve girin **ADL: listesi depolama yolu**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-294">Open hello command palette (Ctrl+Shift+P) and enter **ADL: List Storage Path**.</span></span>

    ![Visual Studio Code listesi depolama birimi yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  <span data-ttu-id="5ca3c-296">Merhaba depolama yolu listeleme, tercih edilen yol seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-296">Select your preferred way for listing hello storage path.</span></span> <span data-ttu-id="5ca3c-297">Bu oluşturularak kullanan **bir yol girin** bir örnek olarak.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-297">This passage uses **Enter a path** as an example.</span></span>

    ![Visual Studio Code tek yönlü toolist hello depolama birimi yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- <span data-ttu-id="5ca3c-299">VS Code her Data Lake Analytics hesabı hello son ziyaret edilen yolu tutar.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-299">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="5ca3c-300">Örneğin: / tt/sn.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-300">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="5ca3c-301">Kök yolu tarayıcısından: hello listesi kök yolu, seçilen Data Lake Analytics hesabı veya yerel bir yol.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-301">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="5ca3c-302">Bir yol girin: Seçili Data Lake Analytics hesabınızı belirtilen yoldan veya yerel bir yol listesi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-302">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>
    
3. <span data-ttu-id="5ca3c-303">Bir hesap hello yerel yol veya bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-303">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Daha fazla bilgi için Visual Studio Code Data Lake araçları seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. <span data-ttu-id="5ca3c-305">Seçin **daha fazla** toolist daha fazla Data Lake Analytics hesapları ve Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-305">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

    ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  <span data-ttu-id="5ca3c-307">Bir Azure depolama yolunu girin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-307">Enter an Azure storage path.</span></span> <span data-ttu-id="5ca3c-308">Örneğin, / çıktı.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-308">For example, /output.</span></span>

    ![Data Lake araçları Visual Studio Code için depolama alanı yolu girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  <span data-ttu-id="5ca3c-310">Sonuçları: hello komutu palet girişlerini temel alarak hello yol bilgileri listeler.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-310">Results: hello command palette lists hello path information based on your entries.</span></span>

    ![Data Lake araçları Visual Studio Code için depolama birimi yolu sonuçları listesi](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

<span data-ttu-id="5ca3c-312">Toolist hello göreli yol hello olup daha kolay bir yol bağlam menüsü sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-312">A more convenient way toolist hello relative path is through hello right-click context menu.</span></span>

<span data-ttu-id="5ca3c-313">**toolist hello depolama yolundan sağ tıklayın**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-313">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="5ca3c-314">Merhaba yolu dizesi tooselect sağ **listesi depolama yolu**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-314">Right-click hello path string tooselect **List Storage Path**.</span></span>

       ![Visual Studio Code için Data Lake Araçları bağlam menüsü sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. <span data-ttu-id="5ca3c-316">Merhaba seçili göreli yolu hello komutu palette görünür.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-316">hello selected relative path appears in hello command palette.</span></span>

   ![Data Lake araçları Visual Studio Code seçili göreli yolu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  <span data-ttu-id="5ca3c-318">Bir hesap hello yerel yol veya bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-318">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  <span data-ttu-id="5ca3c-320">Sonuçları: hello komutu palet hello klasörleri ve dosyaları hello geçerli yolu için listeler.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-320">Results: hello command palette lists hello folders and files for hello current path.</span></span>

       ![Visual Studio Code listeden hello geçerli yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a><span data-ttu-id="5ca3c-322">Önizleme hello depolama dosyası</span><span class="sxs-lookup"><span data-stu-id="5ca3c-322">Preview hello storage file</span></span>
<span data-ttu-id="5ca3c-323">Merhaba depolama dosyasını sağ tıklatın veya hello komutu palet aracılığıyla önizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-323">You can preview hello storage file through hello command palette or through right-click.</span></span>

<span data-ttu-id="5ca3c-324">**Merhaba komutu palet aracılığıyla toopreview hello depolama dosyası**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-324">**toopreview hello storage file through hello command palette**</span></span>

1.  <span data-ttu-id="5ca3c-325">Merhaba komutu palet (Ctrl + Shift + P) açın ve girin **ADL: Önizleme depolama dosyası**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-325">Open hello command palette (Ctrl+Shift+P) and enter **ADL: Preview Storage File**.</span></span>

       ![Visual Studio Code Önizleme depolama dosyası için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  <span data-ttu-id="5ca3c-327">Bir hesap hello yerel yol veya bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-327">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Visual Studio Code için Data Lake araçları hesabı listesi](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="5ca3c-329">Seçin **daha fazla** toolist daha fazla Data Lake Analytics hesapları ve Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-329">Select **more** toolist more Data Lake Analytics accounts, and then select a Data Lake Analytics account.</span></span>

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  <span data-ttu-id="5ca3c-331">Bir Azure depolama alanı yolu veya dosya girin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-331">Enter an Azure storage path or file.</span></span> <span data-ttu-id="5ca3c-332">Örneğin, /output/SearchLog.txt.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-332">For example, /output/SearchLog.txt.</span></span>

       ![Data Lake araçları Visual Studio Code için depolama birimi yolu ve dosya girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  <span data-ttu-id="5ca3c-334">Sonuçları: hello komutu palet girişlerini temel alarak hello yol bilgileri listeler.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-334">Results: hello command palette lists hello path information based on your entries.</span></span>

       ![Visual Studio Code için Data Lake araçları dosya sonucu Önizleme](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

<span data-ttu-id="5ca3c-336">**toolist hello depolama yolundan sağ tıklayın**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-336">**toolist hello storage path through right-click**</span></span>

1.  <span data-ttu-id="5ca3c-337">bir dosya toopreview hello dosya yolu sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-337">toopreview a file, right-click hello file path.</span></span>

   ![Visual Studio Code için Data Lake Araçları bağlam menüsü sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  <span data-ttu-id="5ca3c-339">Bir hesap hello yerel yol veya bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-339">Select an account from hello local path or a Data Lake Analytics account.</span></span>

       ![Data Lake araçları Visual Studio Code için bir hesap seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  <span data-ttu-id="5ca3c-341">Sonuçları: VS Code hello dosyasının hello Önizleme sonuçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-341">Results: VS Code displays hello preview results of hello file.</span></span>

       ![Visual Studio Code için Data Lake araçları dosya sonucu Önizleme](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a><span data-ttu-id="5ca3c-343">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="5ca3c-343">Upload a file</span></span> 

<span data-ttu-id="5ca3c-344">Merhaba komutları girerek dosyaları karşıya yükleyebilir **ADL: dosyasını karşıya yükle** veya **ADL: yapılandırma yoluyla dosyasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-344">You can upload files by entering hello commands **ADL: Upload File** or **ADL: Upload File through Configuration**.</span></span>

<span data-ttu-id="5ca3c-345">**tooupload dosyaları yine de hello ADL: karşıya dosya komutu**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-345">**tooupload files though hello ADL: Upload File command**</span></span>
1. <span data-ttu-id="5ca3c-346">Ctrl + Shift + P tooopen hello komutu palet seçin veya hello komut dosyası Düzenleyicisi'ni sağ tıklatın ve ardından girin **dosyasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-346">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File**.</span></span>
2.  <span data-ttu-id="5ca3c-347">tooupload hello dosya, yerel bir yol girin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-347">tooupload hello file, enter a local path.</span></span>

    ![Visual Studio Code için Data Lake araçları yerel yolu girin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. <span data-ttu-id="5ca3c-349">Merhaba yolları listeleme hello depolama yolunun birini seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-349">Select one of hello ways of listing hello storage path.</span></span> <span data-ttu-id="5ca3c-350">Bu oluşturularak kullanan **bir yol girin** bir örnek olarak.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-350">This passage uses **Enter a path** as an example.</span></span>

    ![Visual Studio Code listesi depolama birimi yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- <span data-ttu-id="5ca3c-352">VS Code her Data Lake Analytics hesabı hello son ziyaret edilen yolu tutar.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-352">VS Code keeps hello last-visited path in every Data Lake Analytics account.</span></span> <span data-ttu-id="5ca3c-353">Örneğin: / tt/sn.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-353">For example: /tt/ss.</span></span>
    >- <span data-ttu-id="5ca3c-354">Kök yolu tarayıcısından: hello listesi kök yolu, seçilen Data Lake Analytics hesabı veya yerel bir yol.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-354">Browser from root path: hello list root path from your selected Data Lake Analytics account or a local path.</span></span>
    >- <span data-ttu-id="5ca3c-355">Bir yol girin: Seçili Data Lake Analytics hesabınızı belirtilen yoldan veya yerel bir yol listesi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-355">Enter a path: List a specified path from your selected Data Lake Analytics account or a local path.</span></span>

4. <span data-ttu-id="5ca3c-356">Bir hesap hello yerel yol veya bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-356">Select an account from hello local path or a Data Lake Analytics account.</span></span>

    ![Visual Studio Code için Data Lake araçları depolama sağ tıklayın](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. <span data-ttu-id="5ca3c-358">Bir Azure depolama yolunu girin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-358">Enter an Azure storage path.</span></span> <span data-ttu-id="5ca3c-359">Örneğin: / çıktı.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-359">For example: /output.</span></span>

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. <span data-ttu-id="5ca3c-360">Azure depolama yolunu bulun.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-360">Find your Azure storage path.</span></span> <span data-ttu-id="5ca3c-361">Seçin **geçerli klasörü seç**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-361">Select **Choose current folder**.</span></span>

    ![Data Lake araçları Visual Studio Code için bir klasör seçin](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  <span data-ttu-id="5ca3c-363">Sonuçları: Merhaba **çıkış** penceresinde hello dosya karşıya yükleme durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-363">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Visual Studio Code için Data Lake araçları karşıya yükleme durumu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

<span data-ttu-id="5ca3c-365">**tooupload dosyaları yine de hello ADL: yapılandırma komutu aracılığıyla dosyasını karşıya yükle**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-365">**tooupload files though hello ADL: Upload File through Configuration command**</span></span>
1.  <span data-ttu-id="5ca3c-366">Ctrl + Shift + P tooopen hello komutu palet seçin veya hello komut dosyası Düzenleyicisi'ni sağ tıklatın ve ardından girin **yapılandırma yoluyla dosyasını karşıya yükle**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-366">Select Ctrl+Shift+P tooopen hello command palette or right-click hello script editor, and then enter **Upload File through Configuration**.</span></span>
2.  <span data-ttu-id="5ca3c-367">VS Code'da JSON dosyasını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-367">VS Code displays a JSON file.</span></span> <span data-ttu-id="5ca3c-368">Dosya yolları girin ve hello adresindeki birden çok dosya karşıya yükleme aynı anda.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-368">You can enter file paths and upload multiple files at hello same time.</span></span> <span data-ttu-id="5ca3c-369">Yönergeler hello görüntülenen **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-369">Instructions are displayed in hello **Output** window.</span></span> <span data-ttu-id="5ca3c-370">tooproceed tooupload hello dosyası (Ctrl + S) hello JSON dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-370">tooproceed tooupload hello file, save (Ctrl+S) hello JSON file.</span></span>

       ![Visual Studio Code dosya yolu için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  <span data-ttu-id="5ca3c-372">Sonuçları: Merhaba **çıkış** penceresinde hello dosya karşıya yükleme durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-372">Results: hello **Output** window displays hello file upload status.</span></span>

       ![Visual Studio Code için Data Lake araçları karşıya yükleme durumu](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

<span data-ttu-id="5ca3c-374">Merhaba dosya toostorage olan başka bir şekilde tooupload sağ tıklatma menüsünden hello dosyanın tam yolunu veya hello komut dosyası Düzenleyicisi'nde hello dosyanın göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-374">Another way tooupload a file toostorage is through hello right-click menu on hello file's full path or hello file's relative path in hello script editor.</span></span> <span data-ttu-id="5ca3c-375">Merhaba yerel dosya yolu girin ve ardından hello hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-375">Enter hello local file path, and then select hello account.</span></span> <span data-ttu-id="5ca3c-376">Merhaba **çıkış** penceresinde hello karşıya yükleme durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-376">hello **Output** window displays hello upload status.</span></span> 

### <a name="open-azure-storage-explorer"></a><span data-ttu-id="5ca3c-377">Açık Azure Storage Gezgini</span><span class="sxs-lookup"><span data-stu-id="5ca3c-377">Open Azure Storage Explorer</span></span>
<span data-ttu-id="5ca3c-378">Açabilirsiniz **Azure Storage Gezgini** hello komutu girerek **ADL: Web Azure Storage Gezgini açmak** veya hello sağ bağlam menüsünden seçerek.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-378">You can open **Azure Storage Explorer** by entering hello command **ADL: Open Web Azure Storage Explorer** or by selecting it from hello right-click context menu.</span></span>

<span data-ttu-id="5ca3c-379">**tooopen Azure Storage Gezgini**</span><span class="sxs-lookup"><span data-stu-id="5ca3c-379">**tooopen Azure Storage Explorer**</span></span>

1. <span data-ttu-id="5ca3c-380">Ctrl + Shift + P tooopen hello komutu palet seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-380">Select Ctrl+Shift+P tooopen hello command palette.</span></span>
2. <span data-ttu-id="5ca3c-381">Girin **açık Web Azure Storage Gezgini** veya göreli bir yol veya hello komut dosyası Düzenleyicisi'nde hello tam yolu sağ tıklayın ve ardından **açık Web Azure Storage Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-381">Enter **Open Web Azure Storage Explorer** or right-click on a relative path or hello full path in hello script editor, and then select **Open Web Azure Storage Explorer**.</span></span>
3. <span data-ttu-id="5ca3c-382">Bir Data Lake Analytics hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-382">Select a Data Lake Analytics account.</span></span>

<span data-ttu-id="5ca3c-383">Data Lake araçları hello Azure portal hello Azure depolama yol açar.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-383">Data Lake Tools opens hello Azure storage path in hello Azure portal.</span></span> <span data-ttu-id="5ca3c-384">Merhaba dosyasından yolu ve önizleme hello hello web bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-384">You can find hello path and preview hello file from hello web.</span></span>

### <a name="local-run-and-local-debug-for-windows-users"></a><span data-ttu-id="5ca3c-385">Yerel çalıştırma ve yerel kullanıcılar için Windows hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="5ca3c-385">Local run and local debug for Windows users</span></span>
<span data-ttu-id="5ca3c-386">U-SQL yerel çalıştırma yerel verilerinizi sınar ve kodunuzu yayımlanan tooData Lake Analytics önce komut yerel olarak doğrular.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-386">U-SQL local run tests your local data and validates your script locally, before your code is published tooData Lake Analytics.</span></span> <span data-ttu-id="5ca3c-387">kodunuzu önce aşağıdaki görevler, toocomplete hello tooData Lake Analytics gönderilen hello yerel hata ayıklama özellik sağlar:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-387">hello local debug feature enables you toocomplete hello following tasks before your code is submitted tooData Lake Analytics:</span></span> 
- <span data-ttu-id="5ca3c-388">C# arka plan kod hata ayıklaması.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-388">Debug your C# code-behind.</span></span> 
- <span data-ttu-id="5ca3c-389">Merhaba kod üzerinden adım.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-389">Step through hello code.</span></span> 
- <span data-ttu-id="5ca3c-390">Komut dosyası yerel olarak doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-390">Validate your script locally.</span></span>

<span data-ttu-id="5ca3c-391">Yerel çalıştırma ve yerel hata ayıklama hakkında yönergeler için bkz: [U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-391">For instructions on local run and local debug, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>

## <a name="additional-features"></a><span data-ttu-id="5ca3c-392">Ek Özellikler</span><span class="sxs-lookup"><span data-stu-id="5ca3c-392">Additional features</span></span>

<span data-ttu-id="5ca3c-393">VS Code'da için Data Lake araçları hello aşağıdaki özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-393">Data Lake Tools for VS Code supports hello following features:</span></span>

-   <span data-ttu-id="5ca3c-394">IntelliSense otomatik tamamlama: önerileri anahtar sözcükler, yöntemleri ve değişkenler gibi öğelerin etrafında açılır pencere görünür.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-394">IntelliSense auto-complete: Suggestions appear in pop-up windows around items, such as keywords, methods, and variables.</span></span> <span data-ttu-id="5ca3c-395">Farklı simgeler farklı hello nesne türlerini temsil eder:</span><span class="sxs-lookup"><span data-stu-id="5ca3c-395">Different icons represent different types of hello objects:</span></span>

    - <span data-ttu-id="5ca3c-396">Scala veri türü</span><span class="sxs-lookup"><span data-stu-id="5ca3c-396">Scala data type</span></span>
    - <span data-ttu-id="5ca3c-397">karmaşık veri türü</span><span class="sxs-lookup"><span data-stu-id="5ca3c-397">Complex data type</span></span>
    - <span data-ttu-id="5ca3c-398">Yerleşik atama</span><span class="sxs-lookup"><span data-stu-id="5ca3c-398">Built-in UDTs</span></span>
    - <span data-ttu-id="5ca3c-399">.NET koleksiyonu ve sınıfları</span><span class="sxs-lookup"><span data-stu-id="5ca3c-399">.NET collection and classes</span></span>
    - <span data-ttu-id="5ca3c-400">C# ifadeleri</span><span class="sxs-lookup"><span data-stu-id="5ca3c-400">C# expressions</span></span>
    - <span data-ttu-id="5ca3c-401">Yerleşik C# UDF'ler, Udo'lar ve UDAAGs</span><span class="sxs-lookup"><span data-stu-id="5ca3c-401">Built-in C# UDFs, UDOs, and UDAAGs</span></span> 
    - <span data-ttu-id="5ca3c-402">U-SQL işlevleri</span><span class="sxs-lookup"><span data-stu-id="5ca3c-402">U-SQL functions</span></span>
    - <span data-ttu-id="5ca3c-403">U-SQL Pencereleme işlevi</span><span class="sxs-lookup"><span data-stu-id="5ca3c-403">U-SQL windowing function</span></span>
 
    ![Visual Studio kod IntelliSense nesne türleri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   <span data-ttu-id="5ca3c-405">IntelliSense otomatik tamamlama Data Lake Analytics meta: Data Lake araçları hello Data Lake Analytics meta veri bilgileri yerel olarak indirir.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-405">IntelliSense auto-complete on Data Lake Analytics metadata: Data Lake Tools downloads hello Data Lake Analytics metadata information locally.</span></span> <span data-ttu-id="5ca3c-406">Merhaba IntelliSense özelliği hello veritabanı, şema, tablo, görünüm, Tablo Değerli Fonksiyon, yordamlar ve hello Data Lake Analytics meta verilerden C# derlemeleri, nesneleri otomatik olarak doldurur.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-406">hello IntelliSense feature automatically populates objects, including hello database, schema, table, view, table-valued function, procedures, and C# assemblies, from hello Data Lake Analytics metadata.</span></span>
 
    ![Visual Studio kod IntelliSense meta verileri için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   <span data-ttu-id="5ca3c-408">IntelliSense hata işaret: Data Lake araçları hataları U-SQL ve C# için düzenleme hello altını çizer.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-408">IntelliSense error marker: Data Lake Tools underlines hello editing errors for U-SQL and C#.</span></span> 
-   <span data-ttu-id="5ca3c-409">Sözdizimi vurgular: Data Lake araçları değişkenleri, anahtar sözcükler, veri türü ve işlevleri gibi farklı renkler toodifferentiate öğeleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="5ca3c-409">Syntax highlights: Data Lake Tools uses different colors toodifferentiate items, such as variables, keywords, data type, and functions.</span></span> 

    ![Visual Studio Code sözdizimi için Data Lake araçları vurgular](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a><span data-ttu-id="5ca3c-411">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ca3c-411">Next steps</span></span>

- <span data-ttu-id="5ca3c-412">U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama için bkz: [U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama](data-lake-tools-for-vscode-local-run-and-debug.md).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-412">For U-SQL local run and local debug with Visual Studio Code, see [U-SQL local run and local debug with Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).</span></span>
- <span data-ttu-id="5ca3c-413">Başlama Data Lake Analytics hakkında bilgi için bkz: [Öğreticisi: Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-413">For getting-started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="5ca3c-414">Visual Studio için Data Lake araçları hakkında bilgi için bkz: [öğretici: Visual Studio için Data Lake araçları kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-414">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="5ca3c-415">Derlemeler geliştirme hakkında daha fazla bilgi için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="5ca3c-415">For information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>



