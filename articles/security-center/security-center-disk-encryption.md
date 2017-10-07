---
title: bir Azure sanal makine aaaEncrypt | Microsoft Docs
description: "Bu belgede Azure Güvenlik Merkezi'nden uyarı aldıktan sonra tooencrypt bir Azure sanal makine sağlar."
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>Azure Sanal Makine'yi şifreleme
Şifrelenmemiş sanal makineleriniz varsa Azure Güvenlik Merkezi sizi uyarır. Bu uyarılar yüksek önem derecesi ve hello öneri olarak gösterecektir bu sanal makinelerin tooencrypt şeklindedir.

![Disk şifreleme önerisi](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> Bu belgedeki bilgiler Hello (Azure Yedekleme'yi kullanarak sanal makineleri yedekleme için gerekli olan) bir anahtar şifreleme anahtarı kullanmadan tooencrypting sanal makineler geçerlidir. Lütfen hello makalesine bakın [için Azure Disk şifrelemesi Windows ve Linux Azure sanal makineleri](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) hakkında bilgi için toouse anahtar şifreleme anahtarı toosupport Azure Backup şifrelenmiş Azure Virtual Machines için.
>
>

Azure Güvenlik Merkezi tarafından şifreleme gerektiği belirlenen Azure Virtual Machines tooencrypt hello aşağıdaki adımları öneririz:

* Azure PowerShell'i yükleyip yapılandırın. Bu, toorun hello PowerShell komutları gerekli tooset hello önkoşullar gerekli tooencrypt Azure sanal makineleri yedeklemek olanak tanır.
* Edinin ve hello Azure Disk şifrelemesi önkoşulları Azure PowerShell betiğini çalıştırın
* Sanal makinelerinizi şifreleyin

Merhaba, bu belgenin hedeftir tooenable, tooencrypt Azure PowerShell'de çok az kayıpla veya hiç arka plana sahip olsa bile, sanal makineleriniz.
Bu belge, Azure Disk şifrelemesi yapılandıracağınız hello istemci makine gibi Windows 10 kullandığınızı varsayar.

Kullanılan toosetup hello önkoşulları ve tooconfigure şifreleme Azure Virtual Machines için birçok yaklaşım vardır. Zaten Azure PowerShell veya Azure CLI bilgiliyseniz, toouse alternatif yaklaşımlar tercih edebilirsiniz.

> [!NOTE]
> Azure sanal makineleri için alternatif yaklaşımlar tooconfiguring şifreleme hakkında daha fazla toolearn lütfen bkz. [için Azure Disk şifrelemesi Windows ve Linux Azure sanal makineleri](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).
>
>

## <a name="install-and-configure-azure-powershell"></a>Azure PowerShell'i yükleyip yapılandırma
Bilgisayarınızda Azure PowerShell 1.2.1 sürümü veya üstünün yüklü olması gerekir. Merhaba makale [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) Azure PowerShell ile bilgisayar toowork tooprovision gereken tüm hello adımları içerir. Merhaba en kolay yaklaşım toouse hello Web PI Kurulumu yaklaşımını bu makalede değinilen olur. Azure PowerShell önceden yüklü olsa bile yüklü, böylece Azure PowerShell'in en son sürümünü hello sahip hello Web PI yaklaşımını kullanarak yeniden yükleyin.

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>Edinin ve hello Azure disk şifrelemesi önkoşulları yapılandırma betiğini çalıştırın
Azure sanal makinelerinizi şifrelemek için gereken tüm hello Önkoşullar Hello Azure Disk şifrelemesi önkoşulları yapılandırma betiği ayarlayacaksınız.

1. Merhaba sahip gidin toohello GitHub sayfası [Azure Disk şifrelemesi önkoşulları Kurulum betiği](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
2. Merhaba Hello GibHub sayfasında, tıklatın **Raw** düğmesi.
3. Kullanmak **CTRL-A** tooselect tüm hello hello sayfasında metin ve ardından **CTRL-C** toocopy tüm metin hello sayfa toohello Panosu'nda hello.
4. Açık **not defteri** ve hello kopyalanan metni Not Defteri'ne yapıştırın.
5. C: sürücünüzde **AzureADEScript** adlı yeni bir klasör oluşturun.
6. Merhaba not defteri dosyasını kaydedin; tıklatın **dosya**, ardından **Kaydet**. Merhaba dosya adı metin kutusuna girin **"ADEPrereqScript.ps1"** tıklatıp **kaydetmek**. (Merhaba adını tırnak işaretleri içine hello put emin olun, aksi takdirde, hello dosya .txt dosya uzantısıyla kaydeder).

Merhaba betik içeriği kaydedildiğine göre hello betik hello PowerShell ISE açın:

1. Hello Başlat menüsü, tıklatın **Cortana**. Sorun **Cortana** yazarak "PowerShell" **PowerShell** hello Cortana arama metin kutusuna.
2. **Windows PowerShell ISE**'ye sağ tıklayın ve **Yönetici olarak çalıştır**'a tıklayın.
3. Merhaba, **yönetici: Windows PowerShell ISE** penceresinde tıklatın **Görünüm** ve ardından **betik bölmesini göster**.
4. Merhaba görürseniz **komutları** bölmesi hello penceresinde hello sağ tarafındaki hello **"x"** hello sağ üst köşesinde hello bölmesini tooclose, onu. Merhaba metin, toosee kadar küçükse kullanmak **CTRL + Ekle** ("Merhaba ekleyin" "+" imzalamak). Hello metin çok büyükse kullanmak **CTRL + çıkar** (çıkarma olduğu hello "-" işareti).
5. **Dosya**'ya tıklayın ve ardından **Aç**'a tıklayın. Toohello gidin **C:\AzureADEScript** klasörü ve hello çift hello üzerinde **ADEPrereqScript**.
6. Merhaba **ADEPrereqScript** içeriği hello PowerShell ISE artık görünür olmalıdır ve ren kodlu toohelp gördüğünüz komutlar, parametreler ve değişkenler gibi çeşitli bileşenleri daha kolay olan.

Şimdi aşağıdaki şekilde hello gibi bir şey görmeniz gerekir.

![PowerShell ISE penceresi](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

Hello üst bölme "betik bölmesi" başvurulan tooas hello ve hello alt bölme başvurulan tooas hello "konsol". Daha sonra bu makalede bu terimleri kullanacağız.

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>Hello Azure disk şifrelemesi önkoşulları PowerShell komutunu çalıştırın
Hello Azure Disk şifrelemesi önkoşulları betiği hello betik başlattıktan sonra aşağıdaki bilgilerle Merhaba ister:

* **Kaynak grubu adı** - ad hello tooput istediğiniz kaynak grubunu anahtar kasasını hello.  Hiç yoksa önceden oluşturulan bu ada sahip yeni bir kaynak grubu girdiğiniz hello adıyla oluşturulur. Bu abonelikte toouse istediğiniz bir kaynak grubu zaten varsa, hello bu kaynak grubunun adını girin.
* **Anahtar kasasının adı** -şifreleme anahtarlarının olduğundan yerleştirilen toobe hello anahtar kasası adı. Bu ada sahip bir Anahtar Kasanız zaten yoksa bu ad ile yeni bir Anahtar Kasası oluşturulur. Toouse istediğiniz bir anahtar kasası zaten varsa, anahtar kasası varolan hello hello adını girin.
* **Konum** -hello anahtar kasası konumu. Şifrelenmiş hello anahtar kasası ve VM'lerin toobe hello olduğundan emin olun aynı konumu. Başlangıç konumu bilmiyorsanız, adım vardır, bunu nasıl yapacağınızı gösterir bu makalenin sonraki bölümlerinde toofind çıkışı.
* **Azure Active Directory Uygulama adı** -hello kullanılan toowrite gizli toohello anahtar kasası olacak Azure Active Directory Uygulama adı. Bu ada sahip bir uygulama yoksa yeni bir uygulama oluşturulur. Toouse istediğiniz bir Azure Active Directory uygulaması zaten varsa bu Azure Active Directory Uygulama hello adını girin.

> [!NOTE]
> Toowhy merak ediyorsanız toocreate bir Azure Active Directory uygulaması gereken Lütfen bakın *bir uygulamayı Azure Active Directory ile kaydetme* hello makalenin bölümünde [Azure anahtar kasasıileçalışmayabaşlama](../key-vault/key-vault-get-started.md).
>
>

Aşağıdaki adımları tooencrypt bir Azure sanal makine hello gerçekleştirin:

1. Merhaba PowerShell ISE'yi kapattıysanız yükseltilmiş hello PowerShell ISE örneği açın. PowerShell ISE zaten değil hello açarsanız, bu makalenin hello yönergeleri izleyin. Hello betiği kapattıysanız hello açmak **ADEPrereqScript.ps1** tıklatarak **dosya**, ardından **açmak** ve hello hello betiği seçerek **c:\ AzureADEScript** klasör. Merhaba başlangıçtan bu makalede izlediyseniz yalnızca toohello sonraki adımda taşıyın.
2. Merhaba PowerShell ISE (alt bölmesinden hello PowerShell ISE hello) Hello konsolunda hello odak toohello yerel hello komut yazarak değiştirme **cd c:\AzureADEScript** ve basın **ENTER**.
3. Merhaba komut çalıştırabilmeniz için makinenizde hello yürütme ilkesini ayarlayın. Tür **Set-ExecutionPolicy Unrestricted** hello konsol ve ardından ENTER tuşuna basın. Merhaba değişiklik tooexecution İlkesi hello etkileri hakkında bildiren bir iletişim kutusu görürseniz, tıklayın **Evet tooall** veya **Evet** (görürseniz **Evet tooall**, varsa bu seçeneği belirleyin görmezseniz **Evet tooall**, ardından **Evet**).
4. Azure hesabınızda oturum açın. Merhaba konsolunda yazın **Login-AzureRmAccount** ve basın **ENTER**. Kimlik bilgilerinizi girin bir iletişim kutusu görüntülenir (hakları toochange hello sanal makineleri olduğundan emin olun hakları yoksa mümkün tooencrypt olmaz bunları. Emin değilseniz aboneliğinizin sahibine veya yöneticinize sorun). **Environment**, **Account**, **TenantId**, **SubscriptionId** ve **CurrentStorageAccount**'ınız hakkında bilgiler görmeniz gerekir. Kopya hello **Subscriptionıd** tooNotepad. #6. adımda bu toouse gerekir.
5. Sanal makinenizin hangi aboneliğin tooand konumuna aittir. Çok Git[https://portal.azure.com](ttps://portal.azure.com) ve oturum açın.  Yan hello sayfasının sol hello üzerinde tıklatın **sanal makineleri**. Sanal makineler ve ait hello Aboneliklerin listesini görürsünüz.

   ![Virtual Machines](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. PowerShell ISE toohello döndürür. Merhaba betiğin çalıştırılacağı hello abonelik bağlamını ayarlayın. Merhaba konsolunda yazın **Select-AzureRmSubscription – Subscriptionıd < your_subscription_ıd >** (Değiştir **< your_subscription_ıd >** değerini gerçek abonelik kimliğinizle) ve tuşunabasın** GİRİN**. Merhaba ortamı hakkında bilgi görürsünüz **hesap**, **Tenantıd**, **Subscriptionıd** ve **CurrentStorageAccount**.
7. Hazır toorun hello betik sunulmuştur. Hello tıklatın **komut dosyasını Çalıştır** düğmesini veya basın **F5** hello klavyede.

   ![PowerShell Betiğini Yürütme](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. Merhaba betik sorar **resourceGroupName:** -hello adını girin *kaynak grubu* toouse, istediğiniz tuşuna basarak **ENTER**. Yoksa, yeni bir toouse istediğiniz bir ad girin. Zaten varsa bir *kaynak grubu* (örneğin, sanal makine hello biri) toouse istiyorsanız, mevcut kaynak grubunun hello hello adını girin.
9. Hello betik sorar **keyVaultName:** -hello hello adını *anahtar kasası* toouse istediğiniz ve ardından ENTER tuşuna basın. Yoksa, yeni bir toouse istediğiniz bir ad girin. Toouse istediğiniz bir anahtar kasası zaten varsa, hello varolan hello adını girin *anahtar kasası*.
10. Merhaba betik sorar **konumu:** - hello hangi hello tooencrypt istediğiniz VM'nin bulunduğu hello konumun adını girin, sonra basın **ENTER**. Başlangıç konumu hatırlamıyorsanız toostep #5 geri dönün.
11. Merhaba betik sorar **aadAppName:** -hello hello adını girin *Azure Active Directory* toouse, istediğiniz uygulama tuşuna **ENTER**. Yoksa, yeni bir toouse istediğiniz bir ad girin. Zaten varsa bir *Azure Active Directory Uygulama* toouse istiyorsanız, var olan hello hello adını girin *Azure Active Directory Uygulama*.
12. İletişim kutusunda bir günlük görüntülenir. Kimlik bilgilerinizi sağlayın (Evet, kere oturum açtınız ancak şimdi toodo gerekir tekrar).
13. Merhaba betik çalışır ve tamamlandığında onu hello toocopy hello değerlerini ister **Aadclientıd**, **aadClientSecret**, **diskEncryptionKeyVaultUrl**ve **Keyvaultresourceıd**. Her bu değerleri toohello panoya kopyalayın ve Not Defteri'ne yapıştırın.
14. PowerShell ISE toohello dönün ve hello imleç hello sonuna hello son satır ve tuşuna yerleştirin **ENTER**.

Merhaba betik Hello çıktısını Merhaba ekranında aşağıdaki gibi görünmelidir:

![PowerShell çıkışı](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>Hello Azure sanal makinesini şifrelemek
Sanal makineniz şimdi hazır tooencrypt şunlardır. Sanal makineniz bulunuyorsa, anahtar kasanız ile aynı kaynak grubunda toohello şifreleme adımları bölümüne geçebilirsiniz hello. Ancak, sanal makineniz değilse hello aynı kaynak grubu anahtar kasası, tooenter hello aşağıdaki hello PowerShell ISE konsolunda hello gerekir:

**$resourceGroupName = <’Virtual_Machine_RG’>**

Değiştir **< Virtual_Machine_RG >** hello kaynak sanal makinelerinizi bulunur grubunuzun hello adıyla tek bir tırnakla çevrelenmiş şekilde değiştirin. Ardından **ENTER**'a basın.
Kaynak grubu adının girildiğini doğru Merhaba, hello PowerShell ISE konsolunda hello aşağıdakileri yazın tooconfirm:

**$resourceGroupName**

**ENTER**'a basın. Merhaba, sanal makineleriniz bulunan bir kaynak grubu adını görmeniz gerekir. Örneğin:

![PowerShell çıkışı](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>Şifreleme adımları
Öncelikle, tootell PowerShell hello adı gerekir hello sanal makineye tooencrypt istiyor. Merhaba konsolda şunu yazın:

**$vmName = <’your_vm_name’>**

Değiştir **<'your_vm_name ' >** VM hello adıyla (Merhaba adı tek bir tırnakla çevrelenmiş olduğundan emin olun) ve tuşuna basarak **ENTER**.

VM adı girilmedi doğru Merhaba, yazın tooconfirm:

**$vmName**

**ENTER**'a basın. Merhaba adı görmelisiniz hello sanal makineye tooencrypt istiyor. Örneğin:

![PowerShell çıkışı](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

Merhaba sanal makinede tüm sürücüler iki yöntem toorun hello şifreleme komutu tooencrypt vardır. Hello ilk yöntemi tootype hello hello PowerShell ISE konsolunda komutunda aşağıdaki gibidir:

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

Bu komutu yazdıktan sonra **ENTER**'a basın.

Merhaba ikinci yöntem tooclick hello betik bölmesinde (Merhaba PowerShell ISE hello üst bölmesinde) ve hello betik toohello altındaki aşağı değildir. Yukarıda listelenen hello komutu vurgulayın ve ardından buna sağ tıklayın ve ardından **Seçimi Çalıştır** veya basın **F8** hello klavyede.

![PowerShell ISE](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

Merhaba yönteminden bağımsız olarak, hello işlemi toocomplete 10-15 dakika sürer size bildiren bir iletişim kutusu görünür kullanın. **Evet**'e tıklayın.

Merhaba şifreleme işlemi gerçekleşirken, toohello Azure portalına dönün ve hello hello sanal makinenin durumunu görebilirsiniz. Yan hello sayfasının sol hello üzerinde tıklatın **sanal makineler**, hello sonra **sanal makineler** dikey penceresinde şifrelediğiniz hello sanal makine hello adına tıklayın. Görüntülenen hello dikey penceresinde bu hello fark edeceksiniz **durum** 'un **güncelleştirme**. Bu, şifreleme işleminin gerçekleştiğini gösterir.

![Merhaba VM hakkında daha fazla ayrıntı](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

PowerShell ISE toohello döndürür. Merhaba betik tamamlandığında aşağıdaki hello şekilde görünen görürsünüz.

![PowerShell çıkışı](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

sanal makine hello toodemonstrate artık şifrelenmiş, toohello Azure portalına dönün ve **sanal makineleri** yan hello sayfasının sol hello üzerinde. Şifrelediğiniz sanal makinenin hello Hello adına tıklayın. Merhaba, **ayarları** dikey penceresinde tıklatın **diskleri**.

![Ayarlar seçenekleri](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

Merhaba üzerinde **diskleri** dikey penceresinde göreceksiniz **şifreleme** olan **etkin**.

![Diskler özellikleri](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>Sonraki adımlar
Bu belgede, nasıl öğrenilen tooencrypt bir Azure sanal makine. Azure Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) – nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) -öğrenin nasıl toomanage ve yanıt toosecurity uyarıları
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) – hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz
* [Azure Güvenlik Blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulun
