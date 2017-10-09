---
title: "Azure RemoteApp için bir özel şablon görüntüsü aaaHow toocreate | Microsoft Docs"
description: "Toocreate özel bir şablon görüntü Azure RemoteApp için nasıl öğrenin. Bu şablon bir karma veya Bulut koleksiyonuyla kullanabilirsiniz."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9e3a0b2d3cc56177ea51406e6cecfe19ff235340
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-custom-template-image-for-azure-remoteapp"></a>Nasıl toocreate özel bir şablon görüntü Azure RemoteApp için
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp Kullanıcılarınızla tooshare istediğiniz tüm hello programlar Windows Server 2012 R2 şablon görüntüsünü toohost kullanır. toocreate özel bir RemoteApp şablon görüntüsü, varolan bir görüntüyle başlatın ya da yeni bir tane oluşturun. 

> [!TIP]
> Bir Azure sanal makineden bir görüntü oluşturabilirsiniz biliyor muydunuz? TRUE Öykü ve keser hello süre miktarını da alır tooimport hello görüntü. Merhaba adımları denetleyin [burada](remoteapp-image-on-azurevm.md).
> 
> 

Azure RemoteApp ile kullanılmak üzere karşıya hello görüntüsü için Hello gereksinimleri şunlardır:

* Merhaba görüntü boyutu, MB katları olmalıdır. Tooupload tam katı değil bir görüntü deneyin hello karşıya yükleme başarısız olur.
* Merhaba görüntü boyutu 127 GB olmalıdır ya da daha küçük.
* Bir VHD dosyası üzerinde olmalıdır (VHDX dosyaları [Hyper-V sanal sabit disk sürücüler] şu anda desteklenmiyor).
* Merhaba VHD 2. nesil sanal makine olmaması gerekir.
* Merhaba VHD sabit boyutlu veya dinamik olarak genişletilen olabilir. Bir sabit boyutlu VHD dosyası'den daha az zaman tooupload tooAzure aldığından dinamik olarak genişleyen bir VHD önerilir.
* Merhaba ana önyükleme kaydı (MBR) bölümleme stilini kullanarak Hello disk başlatılması gerekir. Merhaba GUID bölümleme tablosu (GPT) bölümleme stilini desteklenmiyor.
* Merhaba VHD tek bir Windows Server 2012 R2 yüklemesini içermesi gerekir. Windows yüklemesini içeren birden çok birim, ancak yalnızca bir içerebilir.
* Merhaba Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü ve hello Masaüstü Deneyimi özelliği yüklü olmalıdır.
* Merhaba Uzak Masaüstü Bağlantı Aracısı rol gerekir *değil* yüklü olmalıdır.
* Merhaba şifreleme dosya sistemi (EFS) devre dışı bırakılması gerekir.
* Merhaba görüntüsü hello parametrelerini kullanarak bir Sysprep uygulanmış olması gerekir **/oobe / generalize/shutdown** (yapmak kullanmaz hello **/mode:vm** parametresi).
* Bir anlık görüntü zinciri, VHD'den karşıya yükleme desteklenmez.

**Başlamadan önce**

Merhaba hizmet oluşturmadan önce toodo hello aşağıdaki gerekir:

* [Kaydolun](https://azure.microsoft.com/services/remoteapp/) RemoteApp.
* Bir kullanıcı hesabı, Active Directory toouse hello RemoteApp hizmet hesabı oluşturun. Bunu yalnızca makineler toohello etki alanına katılması bu hesap için hello kısıtlayın. Bkz: [Azure Active Directory'yi Yapılandır RemoteApp](remoteapp-ad.md) daha fazla bilgi için.
* Şirket içi ağınız hakkında bilgi toplayın: IP adresi bilgileri ve VPN cihaz ayrıntıları.
* Merhaba yüklemek [Azure PowerShell](/powershell/azure/overview) modülü.
* Toogrant erişmek istediğiniz hello kullanıcılar hakkında bilgi toplayın. Bu, Microsoft hesap bilgileri veya kullanıcılar için Active Directory iş hesabı bilgileri olabilir.

## <a name="create-a-template-image"></a>Şablon görüntüsü oluşturma
Merhaba yüksek düzey adımları toocreate sıfırdan yeni bir şablon görüntüsü şunlardır:

1. Bir Windows Server 2012 R2 güncelleştirme DVD'SİNDEN veya ISO görüntüsü bulun.
2. Bir VHD dosyası oluşturun.
3. Windows Server 2012 R2 yükleyin.
4. Merhaba Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü ve hello Masaüstü Deneyimi özelliğini yükleyin.
5. Uygulamalarınız tarafından gereken ek özellikleri yükleyin.
6. Yükleyin ve uygulamalarınızı yapılandırın. toomake paylaşım uygulamaları daha kolay, tüm uygulama ve tooshare toohello istediğiniz programları ekleme **Başlat** hello görüntüsü, özellikle **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs menüsü.
7. Uygulamalarınızın gereksinim duyduğu ek Windows yapılandırmalara gerçekleştirin.
8. Merhaba şifreleme dosya sistemi (EFS) devre dışı bırakın.
9. **GEREKLİ:** tooWindows güncelleştirme gidin ve tüm önemli güncelleştirmeleri yükleyin.
10. SYSPREP hello resim.

Merhaba yeni bir görüntü oluşturmak için ayrıntılı adımlar şunlardır:

1. Bir Windows Server 2012 R2 güncelleştirme DVD'SİNDEN veya ISO görüntüsü bulun.
2. Disk Yönetimi'ni kullanarak bir VHD dosyası oluşturun.
   
   1. Disk Yönetimi'ni (diskmgmt.msc) başlatın.
   2. 40 GB veya daha fazla boyutu dinamik olarak genişleyen bir VHD oluşturun. (Windows, uygulamaları ve özelleştirmeler için gereken alanı hello miktarı tahmin edin. Merhaba RDSH rolü ve Masaüstü Deneyimi özelliği yüklü olan Windows sunucusu yaklaşık 10 GB alanı gerektirir).
      
      1. Tıklatın **eylem > VHD oluşturma**.
      2. Başlangıç konumu, boyutu ve VHD biçiminde belirtin. Seçin **dinamik olarak genişletilen**ve ardından **Tamam**.
      
      Bu, birkaç saniye boyunca çalışacak. Merhaba VHD oluşturma tamamlandığında, yeni bir disk herhangi bir sürücü harfi olmayan ve "Başlatılmadı" durumda hello Disk Yönetim konsolunda görmeniz gerekir.
      
      * Başlangıç diski (Merhaba ayrılmamış alan değil) sağ tıklatın ve ardından **diski başlatma**. Seçin **MBR** (ana önyükleme kaydı) hello bölüm stili ve ardından olarak **Tamam**.
      * Yeni bir birim oluşturun: ayrılmamış hello sağ tıklayın ve ardından **yeni basit birim**. Başlangıç Sihirbazı'nda hello Varsayılanları kabul edin, ancak hello şablon görüntüsü yüklediğinizde bir sürücü harfi tooavoid olası sorunları atamak emin olun.
      * Merhaba diske sağ tıklayın ve ardından **Detach VHD**.
3. Windows Server 2012 R2 yükleyin:
   
   1. Yeni bir sanal makine oluşturun. Merhaba Hyper-V Yöneticisi'ni veya Hyper-V istemcisi yeni sanal makine sihirbazını kullanın.
      1. Merhaba nesil belirtin sayfasında, **1. nesil**.
      2. Merhaba sanal Hard diske Bağlan sayfasında, seçin **varolan bir sanal sabit diski kullanmak**, toohello hello önceki adımda oluşturduğunuz VHD göz atın.
      3. Merhaba yükleme seçenekleri sayfasında seçin **bir önyükleme CD'si/DVD_ROM bir işletim sistemini yüklemek**ve ardından Merhaba, Windows Server 2012 R2 yükleme medyasının konumunu seçin.
      4. Merhaba Sihirbazı gerekli tooinstall Windows diğer seçenekleri ve uygulamalarınızı seçin. Başlangıç Sihirbazı'nı tamamlayın.
   2. Merhaba Sihirbaz sona erdikten sonra hello sanal makine hello ayarlarını düzenleyin ve diğer gerekli tooinstall Windows ve hello sanal işlemcilerin sayısı gibi programlarınızı değişiklik ve ardından **Tamam**.
   3. Toohello sanal makineye bağlanmak ve Windows Server 2012 R2 yükleyin.
4. Merhaba Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü ve hello Masaüstü Deneyimi özelliğini yükleyin:
   1. Sunucu Yöneticisi'ni başlatın.
   2. Tıklatın **rol ve Özellik Ekle** hello Hoş Geldiniz ekranında veya hello **Yönet** menüsü.
   3. Tıklatın **sonraki** hello başlamadan önce sayfasında.
   4. Seçin **rol tabanlı veya özellik tabanlı yükleme**ve ardından **sonraki**.
   5. Merhaba yerel makine hello listeden seçin ve ardından **sonraki**.
   6. Seçin **Uzak Masaüstü Hizmetleri**ve ardından **sonraki**.
   7. Genişletme **kullanıcı arabirimleri ve altyapısı** seçip **masaüstü deneyimi**.
   8. Tıklatın **Özellik Ekle**ve ardından **sonraki**.
   9. Merhaba Uzak Masaüstü Hizmetleri sayfasında, tıklatın **sonraki**.
   10. Tıklatın **Uzak Masaüstü oturumu ana bilgisayarı**.
   11. Tıklatın **Özellik Ekle**ve ardından **sonraki**.
   12. Merhaba yükleme seçimlerini onaylayın sayfasında, seçin **otomatik olarak yeniden başlatma hello hedef sunucu**ve ardından **Evet** uyarı hello üzerinde yeniden başlatın.
   13. **Yükle**'ye tıklayın. Merhaba bilgisayar yeniden başlatılır.
5. .NET Framework 3.5 hello gibi uygulamalarınızın gerektirdiği ek özellikleri yükleyin. tooinstall hello özellikleri, Hello Ekle roller ve Özellikler Sihirbazı çalıştırın.
6. Yükleyin ve hello programları ve RemoteApp aracılığıyla toopublish istediğiniz uygulamaları yapılandırın.

> [!IMPORTANT]
> Merhaba RDSH rolünü yükleme uygulamaları tooensure yüklemeden önce hello görüntü önce uygulama uyumluluğu ile ilgili tüm sorunları bulunan, tooRemoteApp karşıya yüklendi.
> 
> Bir kısayol tooyour uygulaması emin olun (**.lnk** dosyası) hello görünür **Başlat** menü tüm kullanıcılar (%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs). Ayrıca hello gördüğünüz bu hello simge olun **Başlat** menü olduğu istediğinizi kullanıcılar toosee. Değilse, bunu değiştirin. (Bunu yapmanız *sahip* tooadd hello uygulama toohello Başlat menüsü, ancak kılar çok daha kolay toopublish Merhaba uygulaması Remoteapp'te. Merhaba uygulama yayımlama Aksi takdirde tooprovide hello hello uygulama yükleme yolu vardır.)
> 
> 

1. Uygulamalarınızın gereksinim duyduğu ek Windows yapılandırmalara gerçekleştirin.
2. Merhaba şifreleme dosya sistemi (EFS) devre dışı bırakın. Bir yükseltilmiş komut penceresi komutunda aşağıdaki hello çalıştırın:
   
     Fsutil davranışı disableencryption 1 ayarlama
   
   Alternatif olarak, ayarlama veya aşağıdaki DWORD değeri hello kayıt defterinde hello ekleyin:
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. Görüntünüzü bir Azure sanal makine içinde oluşturuluyorsa hello yeniden adlandırma  **\%windir%\Panther\Unattend.xml** dosya gibi bu daha sonra çalışmasını kullanılan hello karşıya yükleme komut dosyası engeller. Dağıtımınıza toorevert ihtiyaç durumunda hello dosya hala gerekir böylece bu dosya tooUnattend.old hello adını değiştirin.
4. TooWindows güncelleştirme gidin ve tüm önemli güncelleştirmeleri yükleyin. Tüm güncelleştirmeleri Windows Update birden çok kez tooget toorun gerekebilir. (Bazen bir güncelleştirmeyi yüklemek ve bir güncelleştirme bu güncelleştirmeyi gerektirir.)
5. SYSPREP hello resim. Yükseltilmiş bir komut isteminde hello aşağıdaki komutu çalıştırın:
   
   **C:\Windows\System32\sysprep\sysprep.exe / generalize/oobe Shutdown**
   
   **Not:** hello kullanmayın **/mode:vm** bu sanal makine olsa bile SYSPREP komut hello anahtar.

## <a name="next-steps"></a>Sonraki adımlar
Özel şablon görüntünüzü sahip olduğunuza göre bu görüntü tooyour RemoteApp koleksiyonu tooupload gerekir. Koleksiyonunuz makaleleri toocreate aşağıdaki hello Hello bilgileri kullanın:

* [Nasıl toocreate RemoteApp karma koleksiyonu](remoteapp-create-hybrid-deployment.md)
* [Nasıl toocreate RemoteApp bulut koleksiyonu](remoteapp-create-cloud-deployment.md)

