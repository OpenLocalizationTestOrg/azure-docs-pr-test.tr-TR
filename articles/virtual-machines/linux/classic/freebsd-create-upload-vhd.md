---
title: "aaaCreate ve karşıya yükleme FreeBSD VM görüntü | Microsoft Docs"
description: "Bir sanal sabit hello FreeBSD işletim sistemi toocreate bir Azure sanal makinesini içeren disk (VHD) yüklemek ve toocreate bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a>Oluşturun ve FreeBSD VHD tooAzure yükleyin
Bu makalede FreeBSD işletim sistemi toocreate ve karşıya yükleme sanal sabit içeren bir disk (VHD) nasıl hello gösterilmektedir. Karşıya yüklediğiniz sonra kendi görüntü toocreate azure'da sanal makine (VM) olarak kullanabilirsiniz.

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Merhaba Resource Manager modelini kullanarak bir VHD'yi karşıya yükleme hakkında daha fazla bilgi için bkz: [burada](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Ön koşullar
Bu makalede aşağıdaki öğelerindeki hello olduğunu varsayar:

* **Bir Azure aboneliği**--bir hesabınız yoksa yalnızca birkaç dakika içinde bir oluşturabilirsiniz. Bir MSDN aboneliğiniz varsa, bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Aksi takdirde nasıl çok öğrenin[ücretsiz bir deneme hesabı oluşturma](https://azure.microsoft.com/pricing/free-trial/).  
* **Azure PowerShell Araçları**--hello Azure PowerShell modülü yüklenmelidir ve Azure aboneliğinize toouse yapılandırılmış. toodownload hello modülü bkz [Azure indirmeleri](https://azure.microsoft.com/downloads/). Açıklayan bir öğretici nasıl tooinstall ve yapılandırma hello modülü kullanılabilir burada. Kullanım hello [Azure indirmeleri](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.
* **Bir .vhd dosyası yüklü FreeBSD işletim sistemi**--desteklenen FreeBSD işletim sistemi olmalıdır bir yüklü tooa sanal sabit disk. Birden çok araç toocreate .vhd dosyaları mevcut. Örneğin, Hyper-V toocreate hello .vhd dosyası gibi bir sanallaştırma çözümü kullanın ve hello işletim sistemi yükleyin. Tooinstall ve kullanım Hyper-V, nasıl görürüm hakkında yönergeler için [Hyper-V yükleyin ve sanal makine oluşturma](http://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Azure'da Hello yeni VHDX biçimi desteklenmiyor. Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya cmdlet hello [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx). Ayrıca, bir [nasıl hakkında MSDN'de öğretici toouse FreeBSD Hyper-V ile](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).
>
>

Bu görev hello aşağıdaki beş adımları içerir:

## <a name="step-1-prepare-hello-image-for-upload"></a>1. adım: hello görüntü karşıya yükleme için hazırlama
Merhaba sanal makinede hello FreeBSD işletim sisteminin yüklü olduğu hello yordamları tamamlayın:

1. DHCP'yi etkinleştirin.

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. SSH etkinleştirin.

    Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun. Varsayılan olarak FreeBSD disk yüklemesinden sonra etkin. 
3. Bir seri Konsolu ayarlayın.

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. Sudo yükleyin.

    Azure'da Hello kök hesabı devre dışı. Başka bir deyişle, yükseltilmiş ayrıcalıklarla bir ayrıcalıksız kullanıcı toorun komutlarındaki tooutilize sudo gerekir.

        # pkg install sudo
   
5. Azure Aracısı önkoşulları.

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. Azure aracısını yükleyin.

    Merhaba hello Azure Aracısı en son sürümü her zaman bulunabilir [github](https://github.com/Azure/WALinuxAgent/releases). sürüm 2.0.10 hello + resmi olarak FreeBSD 10 & 10.1 ve 2.1.4 + (2.2.x dahil) resmi olarak destekleyen FreeBSD 10.2 ve sonraki sürümlerinde hello sürümünü destekler.

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    2.0 için 2.0.16 örnek olarak kullanalım:

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    2.1 için şimdi bir örnek olarak 2.1.4 kullanabilirsiniz:

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > Azure aracısını yükledikten sonra çalışan bir fikir tooverify şöyledir:
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. Merhaba sistem sağlamayı sonlandırın.

    Deprovision hello sistem tooclean ve yapma, sağlama işleminin için uygun. Hello aşağıdaki komut da hello son sağlanan kullanıcı hesabını ve ilişkili hello verileri siler:

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    Şimdi, VM kapatma.

## <a name="step-2-create-a-storage-account-in-azure"></a>2. adım: Azure depolama hesabı oluşturma
Kullanılan toocreate bir sanal makine olabilir için Azure tooupload bir .vhd dosyası depolama hesabı olması gerekir. Hello Azure Klasik portalı toocreate bir depolama hesabı kullanabilirsiniz.

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba komut çubuğunda seçin **yeni**.
3. Seçin **Veri Hizmetleri** > **depolama** > **hızlı Oluştur**.

    ![Hızlı bir depolama hesabı oluşturma](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. Aşağıdaki gibi Hello alanları doldurun:

   * Merhaba, **URL** alan, bir alt etki alanı adı toouse hello depolama hesabı URL'si yazın. Merhaba girişi 3-24 sayılar ve küçük harfleri içerebilir. Bu ad kullanılan tooaddress Azure Blob storage, Azure kuyruk depolama ya da Azure Table storage kaynaklarını hello abonelik için hello URL'de hello ana bilgisayar adı olur.
   * Merhaba, **konum/benzeşim grubu** açılır menü hello seçin **konumu ya da benzeşim grubu** hello depolama hesabı için. Bir benzeşim grubu, bulut Hizmetleri ve depolama hello yerleştirmenizi sağlar aynı veri merkezinde.
   * Merhaba, **çoğaltma** alan, karar olup olmadığını toouse **coğrafi olarak yedekli** hello depolama hesabı için çoğaltma. Coğrafi çoğaltma varsayılan olarak açıktır. Bu seçenek, veri tooa ikincil konumda, maliyet tooyou çoğaltır, böylece önemli bir hata durumunda toothat konum depolama alanınızın başarısız hello birincil konumda oluşur. Merhaba ikincil konum otomatik olarak atanır ve değiştirilemez. Son toolegal gereksinimleri veya kuruluş ilkesi, bulut tabanlı depolama hello konumu hakkında daha fazla denetime ihtiyacınız varsa, coğrafi çoğaltma kapatabilirsiniz. Ancak, daha sonra coğrafi çoğaltma üzerinde kapatırsanız, size bir kerelik ücretlendirilir olduğunu unutmayın veri aktarımı ücreti tooreplicate, var olan veri toohello ikincil konum. Depolama Hizmetleri coğrafi çoğaltma olmadan indirimli fiyatla sunulur. Coğrafi çoğaltma depolama hesaplarını yönetme hakkında daha fazla bilgi şurada bulunabilir: [Azure Storage çoğaltma](../../../storage/common/storage-redundancy.md).

     ![Depolama hesabı ayrıntılarını girin](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. Seçin **depolama hesabı oluşturma**. Merhaba hesabı artık altında görünür **depolama**.

    ![Depolama hesabı başarıyla oluşturuldu](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. Ardından, karşıya yüklenen .vhd dosyaları için bir kapsayıcı oluşturun. Merhaba depolama hesabı adı seçin ve ardından **kapsayıcıları**.

    ![Depolama hesabı ayrıntısı](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. Seçin **bir kapsayıcı oluşturmak**.

    ![Depolama hesabı ayrıntısı](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. Merhaba, **adı** alanında, kapsayıcı için bir ad yazın. Ardından hello **erişim** ne tür istediğiniz erişim ilkesi aşağı açılan menüsünde seçin.

    ![Kapsayıcı adı](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > Varsayılan olarak, hello kapsayıcı özeldir ve yalnızca hello hesap sahibi tarafından erişilebilir. Merhaba kapsayıcı, ancak toohello kapsayıcı özellikleri ve meta verileri, tooallow herkese okuma erişimi toohello BLOB'ları kullanmak hello **ortak Blob** seçeneği. tooallow tam ortak okuma erişiminin hello kapsayıcı ve bloblarını, kullanımı için hello **ortak kapsayıcı** seçeneği.
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a>3. adım: hello bağlantı tooAzure hazırlama
Bir .vhd dosyası yükleyebilir önce bilgisayarınız ve Azure aboneliğiniz arasında tooestablish güvenli bir bağlantı gerekir. Hello Azure Active Directory (Azure AD) yöntemini kullanın veya sertifika yöntemi toodo Merhaba.

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a>Hello Azure AD yöntemi tooupload bir .vhd dosyası kullanın
1. Açık hello Azure PowerShell Konsolu.
2. Merhaba aşağıdaki komutu yazın:  
    `Add-AzureAccount`

    Bu komut, bir oturum açma penceresi burada iş veya Okul hesabınızla oturum açar.

    ![PowerShell penceresi](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. Azure kimliğini doğrular ve hello kimlik bilgileri kaydeder. Ardından hello penceresini kapatır.

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a>Merhaba sertifika yöntemi tooupload bir .vhd dosyası kullanın
1. Açık hello Azure PowerShell Konsolu.
2. Tür: `Get-AzurePublishSettingsFile`.
3. Bir tarayıcı penceresi açar ve, toodownload hello .publishsettings dosyasını ister. Bu dosya bilgileri ve Azure aboneliğiniz için bir sertifika içerir.

    ![Tarayıcı indirme sayfası](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. Merhaba .publishsettings dosyasını kaydedin.
5. Tür: `Import-AzurePublishSettingsFile <PathToFile>`, burada `<PathToFile>` hello tam yolu toohello .publishsettings dosyasıdır.

   Daha fazla bilgi için bkz: [Azure cmdlet'leri kullanmaya başlama](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).

   Yükleme ve PowerShell yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

## <a name="step-4-upload-hello-vhd-file"></a>4. adım: hello .vhd dosyasını karşıya yükle
İçinde Blob Depolama alanınızın hello .vhd dosyasını karşıya yüklediğinde, herhangi bir yere yerleştirebilirsiniz. Merhaba dosyasını karşıya yüklediğinde kullanacağınız bazı şartları şunlardır:

* **BlobStorageURL** 2. adımda oluşturduğunuz hello depolama hesabı için hello URL'dir.
* **YourImagesFolder** hello Blob storage içinde istediğiniz yere toostore görüntülerinizi kapsayıcıdır.
* **VHDName** hello Azure Klasik portalı tooidentify hello sanal sabit disk görünen hello etiket.
* **PathToVHDFile** hello .vhd dosyası hello tam yolu ve adıdır.

Merhaba önceki adımda kullanılan hello Azure PowerShell penceresinden yazın:

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a>5. adım: hello karşıya yüklenen .vhd dosyası bir VM oluşturma
Merhaba .vhd dosyası yükledikten sonra aboneliğinizle ilişkili olan ve bu özel görüntü ile bir sanal makine oluşturmak özel görüntülerin görüntü toohello listesi olarak ekleyebilirsiniz.

1. Merhaba önceki adımda kullanılan hello Azure PowerShell penceresinden yazın:

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > Linux hello işletim sistemi türü olarak kullanın. Merhaba geçerli Azure PowerShell sürümü yalnızca "Linux" veya "Windows" parametre olarak kabul eder.
   >
   >
2. Merhaba yukarıdaki adımları tamamladıktan sonra hello seçtiğinizde hello yeni görüntü listelenir **görüntüleri** hello Klasik Azure portalı sekmesinde.  

    ![Bir görüntü seçin](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. Bir sanal makine hello Galerisi'nden oluşturun. Bu yeni görüntüyü artık altında kullanılabilir **görüntülerim**.
4. Merhaba yeni görüntüyü seçin. Ardından, bir ana bilgisayar adı, parola, SSH anahtarı ve benzeri hello istemleri tooset geçer.

    ![Özel görüntü](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. Merhaba sağlama tamamladıktan sonra Azure'da çalışan FreeBSD VM görürsünüz.

    ![Azure FreeBSD görüntüde](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
