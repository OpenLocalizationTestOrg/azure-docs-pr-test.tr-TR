---
title: "aaaInstall Azure Windows VM üzerinde MongoDB | Microsoft Docs"
description: "Windows Server 2012 R2 çalıştıran bir Azure VM üzerinde MongoDB tooinstall hello Resource Manager dağıtım modeli ile nasıl oluşturulacağını öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="9f2f7-103">Yükleme ve Azure Windows VM üzerinde MongoDB yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9f2f7-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="9f2f7-104">[MongoDB](http://www.mongodb.org) bir popüler açık kaynak, yüksek performanslı NoSQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="9f2f7-105">Bu makalede yükleme ve bir Windows Server 2012 R2 sanal makinede (VM) Azure MongoDB yapılandırma sırasında size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="9f2f7-106">Ayrıca [MongoDB azure'da bir Linux VM yüklemek](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="9f2f7-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f2f7-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9f2f7-107">Prerequisites</span></span>
<span data-ttu-id="9f2f7-108">Yükleyip MongoDB yapılandırmadan önce toocreate VM gerekir ve, ideal olarak, bir veri diski tooit ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="9f2f7-109">Aşağıdaki makaleleri toocreate VM hello görmek ve bir veri diski ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="9f2f7-110">Kullanarak bir Windows Server VM oluşturma [Azure portal hello](quick-create-portal.md) veya [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9f2f7-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="9f2f7-111">Bir veri diski tooa Windows Server VM kullanarak attach [Azure portal hello](attach-managed-disk-portal.md) veya [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9f2f7-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="9f2f7-112">Yükleme ve yapılandırma MongoDB, toobegin [tooyour Windows Server VM üzerinde oturum](connect-logon.md) Uzak Masaüstü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="9f2f7-113">MongoDB'yi yükleme</span><span class="sxs-lookup"><span data-stu-id="9f2f7-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9f2f7-114">Kimlik doğrulaması ve IP adresi bağlama gibi MongoDB güvenlik özellikleri varsayılan olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="9f2f7-115">Güvenlik özellikleri, MongoDB tooa üretim ortamına dağıtmadan önce etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="9f2f7-116">Daha fazla bilgi için bkz: [MongoDB güvenlik ve kimlik doğrulama](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="9f2f7-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="9f2f7-117">Uzak Masaüstü kullanarak VM tooyour bağlandıktan sonra Internet Explorer hello açın **Başlat** hello VM menüsünde.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="9f2f7-118">Seçin **kullanım önerilen güvenlik, gizlilik ve uyumluluk ayarları** zaman Internet Explorer ilk açar ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="9f2f7-119">Internet Explorer Artırılmış Güvenlik Yapılandırması, varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="9f2f7-120">Merhaba MongoDB Web sitesi toohello izin verilen siteler listesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="9f2f7-121">Select hello **Araçları** hello sağ üst köşesinde simgesi.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="9f2f7-122">İçinde **Internet Seçenekleri**seçin hello **güvenlik** sekmesini tıklatın ve ardından hello seçin **Güvenilen siteler** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="9f2f7-123">Merhaba tıklatın **siteleri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-123">Click hello **Sites** button.</span></span> <span data-ttu-id="9f2f7-124">Ekleme *https://\*. mongodb.org* Güvenilen siteler ve ardından Kapat hello iletişim kutusu toohello listesi.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![Internet Explorer güvenlik ayarlarını yapılandırın](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="9f2f7-126">Toohello Gözat [MongoDB - indirmeleri](http://www.mongodb.org/downloads) sayfa (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="9f2f7-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="9f2f7-127">Gerekirse, hello seçin **Community Server** edition ve ardından hello en son kararlı sürümü geçerli Windows Server 2008 R2 64-bit ve daha sonra.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="9f2f7-128">toodownload yükleyici Merhaba, tıklatın **yükleme (MSI)**.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![MongoDB yükleyici indirin](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="9f2f7-130">Merhaba yükleme tamamlandıktan sonra hello yükleyiciyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="9f2f7-131">Okuma ve hello lisans sözleşmesini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="9f2f7-132">İstendiğinde, seçin **tam** yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="9f2f7-133">Merhaba son ekranında tıklatın **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="9f2f7-134">Merhaba VM ve MongoDB yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9f2f7-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="9f2f7-135">Merhaba yol değişkenleri hello MongoDB yükleyici tarafından güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="9f2f7-136">Merhaba MongoDB olmadan `bin` path değişkeniniz bir konumda ihtiyacınız toospecify hello tam yolu MongoDB yürütülebilir her kullanışınızda.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="9f2f7-137">tooadd hello konumu tooyour path değişkeni:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="9f2f7-138">Sağ hello **Başlat** menü ve select **sistem**.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="9f2f7-139">Tıklatın **Gelişmiş Sistem ayarları**ve ardından **ortam değişkenleri**.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="9f2f7-140">Altında **sistem değişkenleri**seçin **yolu**ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Yol değişkenleri yapılandırın](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="9f2f7-142">Merhaba yolu tooyour MongoDB ekleme `bin` klasör.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="9f2f7-143">MongoDB yüklü genellikle *C:\Program Files\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="9f2f7-144">VM Hello yükleme yolu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="9f2f7-145">Merhaba aşağıdaki örnek, hello varsayılan MongoDB yükleme konumu toohello `PATH` değişkeni:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="9f2f7-146">Emin tooadd hello başında noktalı virgül olması (`;`) konumu tooyour eklediğiniz tooindicate `PATH` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="9f2f7-147">MongoDB veri ve günlük dizinleri veri diskinizde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="9f2f7-148">Merhaba gelen **Başlat** menüsünde, select **komut istemi**.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="9f2f7-149">Örnek hello hello dizinler F: sürücüde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="9f2f7-150">Aşağıdaki komut, hello yolu tooyour verilerini ayarlama hello ile bir MongoDB örneği başlatın ve dizinleri uygun şekilde oturum:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="9f2f7-151">Merhaba günlük dosyaları MongoDB tooallocate için birkaç dakika sürer ve bağlantıları dinlemeyi Başlat.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="9f2f7-152">Tüm günlük iletilerini yönlendirilmiş toohello olan *F:\MongoLogs\mongolog.log* olarak dosya `mongod.exe` sunucu başlar ve günlük dosyalarını ayırır.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9f2f7-153">MongoDB örneğinizin çalışırken hello komut istemi bu görevde odaklanmış kalır.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="9f2f7-154">Merhaba komut istemi penceresini açık toocontinue MongoDB çalışan bırakın.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="9f2f7-155">Veya hello sonraki adımda ayrıntılı olarak hizmet olarak Mongodb'yi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="9f2f7-156">Merhaba daha sağlam bir MongoDB deneyimi için yükleme `mongod.exe` bir hizmet olarak.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="9f2f7-157">Bir hizmet oluşturma toouse MongoDB her istediğinizde çalışan bir komut istemi tooleave gerekmeyen anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="9f2f7-158">Merhaba, yol tooyour veri ve günlük dizinleri uygun şekilde ayarlama Hello hizmeti aşağıdaki gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="9f2f7-159">Merhaba yukarıdaki komut MongoDB, "Mongo VT" açıklaması ile adlı bir hizmette oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="9f2f7-160">şu parametreler hello da belirtilir:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="9f2f7-161">Merhaba `--dbpath` seçeneği hello hello veri dizininin konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="9f2f7-162">Merhaba `--logpath` seçeneği hello çalışan hizmetin bir komut penceresi toodisplay çıkışını olmadığı için kullanılan toospecify bir günlük dosyası olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="9f2f7-163">Merhaba `--logappend` seçeneği belirtir hello hizmetinin yeniden başlatma çıkış tooappend toohello mevcut günlük dosyası neden olur.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="9f2f7-164">toostart MongoDB hizmet Merhaba, hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="9f2f7-165">Merhaba MongoDB hizmet oluşturma hakkında daha fazla bilgi için bkz: [MongoDB için bir Windows hizmeti yapılandırma](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="9f2f7-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="9f2f7-166">Test hello MongoDB örneği</span><span class="sxs-lookup"><span data-stu-id="9f2f7-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="9f2f7-167">Tek bir örneği olarak çalışan veya bir hizmet olarak yüklü MongoDB ile oluşturma ve kullanma, veritabanlarınızı şimdi başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="9f2f7-168">toostart hello MongoDB Yönetim Kabuğu hello başka bir komut istemi penceresi açın **Başlat** menüsünde ve hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="9f2f7-169">Merhaba hello veritabanlarıyla listeleyebilirsiniz `db` komutu.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="9f2f7-170">Bazı verileri aşağıdaki şekilde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="9f2f7-171">Verileri gibi arayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="9f2f7-172">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="9f2f7-173">Çıkış hello `mongo` gibi konsolu:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="9f2f7-174">Güvenlik Duvarı ve ağ güvenlik grubu kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9f2f7-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="9f2f7-175">MongoDB yüklü ve çalışır durumda, uzaktan tooMongoDB bağlanabilmesi için bir bağlantı noktası Windows Güvenlik Duvarı'nı açın.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="9f2f7-176">toocreate yeni gelen kuralı tooallow TCP bağlantı noktası 27017, yönetici bir PowerShell komut istemini açın ve hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="9f2f7-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="9f2f7-177">Hello kullanarak hello kuralı da oluşturabilirsiniz **Gelişmiş Güvenlik Özellikli Windows Güvenlik Duvarı** grafik yönetim aracıdır.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="9f2f7-178">Yeni gelen kuralı tooallow TCP bağlantı noktası 27017 oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="9f2f7-179">Gerekirse, bir ağ güvenlik grubu kural tooallow erişim tooMongoDB gelen hello mevcut Azure sanal ağ alt dışında oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="9f2f7-180">Hello kullanarak ağ güvenlik grubu kuralları hello oluşturabilirsiniz [Azure portal](nsg-quickstart-portal.md) veya [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9f2f7-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="9f2f7-181">Merhaba Windows Güvenlik duvarı kurallarıyla olarak, TCP bağlantı noktası 27017 toohello sanal ağ arabirimi, MongoDB VM izin verir.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="9f2f7-182">TCP bağlantı noktası 27017 MongoDB tarafından kullanılan hello varsayılan bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="9f2f7-183">Hello kullanarak bu bağlantı noktasını değiştirebilirsiniz `--port` başlatırken parametresi `mongod.exe` el ile veya bir hizmet.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="9f2f7-184">Hello bağlantı noktasını değiştirirseniz, önceki adımları hello emin tooupdate hello Windows Güvenlik Duvarı ve ağ güvenlik grubu kuralları olun.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9f2f7-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9f2f7-185">Next steps</span></span>
<span data-ttu-id="9f2f7-186">Bu öğreticide, nasıl öğrenilen tooinstall ve MongoDB, Windows VM yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f2f7-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="9f2f7-187">Artık MongoDB, Windows VM göre hello konularında Gelişmiş hello aşağıdaki erişebilirsiniz [MongoDB belgelerine](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="9f2f7-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

