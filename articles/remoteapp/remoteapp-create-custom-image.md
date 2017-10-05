---
title: "Azure RemoteApp için özel bir şablon görüntüsü oluşturma | Microsoft Docs"
description: "Azure RemoteApp için özel bir şablon görüntüsü oluşturmayı öğrenin. Bu şablon bir karma veya Bulut koleksiyonuyla kullanabilirsiniz."
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
ms.openlocfilehash: f529a5526f266c7dbac3c719b244d05ab7705941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-custom-template-image-for-azure-remoteapp"></a>Azure RemoteApp için özel bir şablon görüntüsü oluşturma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp, kullanıcılarınız ile paylaşmak istediğiniz tüm programlar barındırmak için bir Windows Server 2012 R2 şablon görüntüsünü kullanır. Özel bir RemoteApp şablon görüntüsü oluşturmak için varolan bir görüntüyle başlatabilir veya yeni bir tane oluşturun. 

> [!TIP]
> Bir Azure sanal makineden bir görüntü oluşturabilirsiniz biliyor muydunuz? Doğru Öykü ve keser süre miktarını bu görüntüyü içe aktarmak için alır. Adımları denetleyin [burada](remoteapp-image-on-azurevm.md).
> 
> 

Azure RemoteApp ile kullanılmak üzere yüklenen görüntü için gereksinimleri şunlardır:

* Görüntü boyutu, MB katları olmalıdır. Tam katı değil görüntüyü karşıya yüklemeye karşıya yükleme başarısız olur.
* Görüntü boyutu 127 GB olmalıdır ya da daha küçük.
* Bir VHD dosyası üzerinde olmalıdır (VHDX dosyaları [Hyper-V sanal sabit disk sürücüler] şu anda desteklenmiyor).
* 2. nesil sanal makine VHD olmamalıdır.
* VHD'yi sabit boyutlu veya dinamik olarak genişletilen olabilir. Azure için bir sabit boyutlu VHD dosyasının karşıya yüklemek için daha az zaman alır çünkü dinamik olarak genişleyen bir VHD önerilir.
* Disk bölümleme stilini ana önyükleme kaydı (MBR) kullanarak başlatılması gerekir. GUID bölümleme tablosu (GPT) bölümleme stilini desteklenmiyor.
* VHD'yi tek bir Windows Server 2012 R2 yüklemesini içermesi gerekir. Windows yüklemesini içeren birden çok birim, ancak yalnızca bir içerebilir.
* Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü ve Masaüstü Deneyimi özelliği yüklü olmalıdır.
* Uzak Masaüstü Bağlantı Aracısı rol gerekir *değil* yüklü olmalıdır.
* Şifreleme Dosya Sistemi (EFS) devre dışı bırakılması gerekir.
* Resmin parametrelerini kullanarak bir Sysprep uygulanmış olması gerekir **/oobe / generalize/shutdown** (vermeyin kullanım **/mode:vm** parametresi).
* Bir anlık görüntü zinciri, VHD'den karşıya yükleme desteklenmez.

**Başlamadan önce**

Hizmet oluşturmadan önce aşağıdakileri yapmanız gerekir:

* [Kaydolun](https://azure.microsoft.com/services/remoteapp/) RemoteApp.
* RemoteApp hizmet hesabı olarak kullanılacak Active Directory'de bir kullanıcı hesabı oluşturun. Bunu yalnızca makine etki alanına katılması bu hesap için kısıtlayın. Bkz: [Azure Active Directory'yi Yapılandır RemoteApp](remoteapp-ad.md) daha fazla bilgi için.
* Şirket içi ağınız hakkında bilgi toplayın: IP adresi bilgileri ve VPN cihaz ayrıntıları.
* Yükleme [Azure PowerShell](/powershell/azure/overview) modülü.
* Erişim vermek istediğiniz kullanıcıları hakkında bilgi toplayın. Bu, Microsoft hesap bilgileri veya kullanıcılar için Active Directory iş hesabı bilgileri olabilir.

## <a name="create-a-template-image"></a>Şablon görüntüsü oluşturma
Sıfırdan yeni bir şablon görüntüsü oluşturmak için üst düzey adımları şunlardır:

1. Bir Windows Server 2012 R2 güncelleştirme DVD'SİNDEN veya ISO görüntüsü bulun.
2. Bir VHD dosyası oluşturun.
3. Windows Server 2012 R2 yükleyin.
4. Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü ve Masaüstü Deneyimi özelliğini yükleyin.
5. Uygulamalarınız tarafından gereken ek özellikleri yükleyin.
6. Yükleyin ve uygulamalarınızı yapılandırın. Paylaşım uygulamaları kolaylaştırmak için herhangi bir uygulama veya paylaşım için istediğiniz program eklemek **Başlat** görüntüsü, özellikle **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs menüsü.
7. Uygulamalarınızın gereksinim duyduğu ek Windows yapılandırmalara gerçekleştirin.
8. Şifreleme Dosya Sistemi (EFS) devre dışı bırakın.
9. **GEREKLİ:** Windows Update sitesine gidin ve tüm önemli güncelleştirmeleri yükleyin.
10. SYSPREP görüntü.

Yeni bir görüntü oluşturmak için ayrıntılı adımlar şunlardır:

1. Bir Windows Server 2012 R2 güncelleştirme DVD'SİNDEN veya ISO görüntüsü bulun.
2. Disk Yönetimi'ni kullanarak bir VHD dosyası oluşturun.
   
   1. Disk Yönetimi'ni (diskmgmt.msc) başlatın.
   2. 40 GB veya daha fazla boyutu dinamik olarak genişleyen bir VHD oluşturun. (Windows, uygulamaları ve özelleştirmeler için gerekli alan miktarı tahmin edin. Masaüstü Deneyimi özelliği yüklü ve RDSH rolü Windows Server yaklaşık 10 GB alanı gerektirir).
      
      1. Tıklatın **eylem > VHD oluşturma**.
      2. Konum, boyutu ve VHD biçiminde belirtin. Seçin **dinamik olarak genişletilen**ve ardından **Tamam**.
      
      Bu, birkaç saniye boyunca çalışacak. VHD oluşturma tamamlandığında, yeni bir disk herhangi bir sürücü harfi olmayan ve "Başlatılmadı" durumda Disk Yönetim konsolunda görmeniz gerekir.
      
      * Disk (ayrılmamış alan değil) sağ tıklayın ve ardından **diski başlatma**. Seçin **MBR** (ana önyükleme kaydı) bölümleme stilini ve ardından olarak **Tamam**.
      * Yeni bir birim oluşturun: ayrılmamış sağ tıklatın ve ardından **yeni basit birim**. Sihirbazdaki varsayılan değerleri kabul edin, ancak şablon görüntüsü yüklediğinizde olası sorunları önlemek için bir sürücü harfi atama emin olun.
      * Diske sağ tıklayın ve ardından **Detach VHD**.
3. Windows Server 2012 R2 yükleyin:
   
   1. Yeni bir sanal makine oluşturun. Hyper-V Yöneticisi'ni veya istemci de Hyper-V yeni sanal makine Sihirbazı'nı kullanın.
      1. Nesil belirtin sayfasında, **1. nesil**.
      2. Sanal Hard diske Bağlan sayfasında, seçin **varolan bir sanal sabit diski kullanmak**ve önceki adımda oluşturduğunuz VHD konumuna göz atın.
      3. Yükleme seçenekleri sayfasında seçin **bir önyükleme CD'si/DVD_ROM bir işletim sistemini yüklemek**ve ardından, Windows Server 2012 R2 yükleme medyasının konumunu seçin.
      4. Sihirbazı'nda Windows ve uygulamalarınızı yüklemek için gerekli diğer seçenekleri seçin. Sihirbazı tamamlayın.
   2. Sihirbaz sona erdikten sonra sanal makine ayarlarını düzenleyin ve diğer değişiklikler Windows ve sanal işlemcilerin sayısı gibi programlarınızı yükleyin ve ardından gerekli **Tamam**.
   3. Sanal makineye bağlanın ve Windows Server 2012 R2 yükleyin.
4. Uzak Masaüstü oturumu ana bilgisayarı (RDSH) rolü ve Masaüstü Deneyimi özelliğini yükleyin:
   1. Sunucu Yöneticisi'ni başlatın.
   2. Tıklatın **rol ve Özellik Ekle** Hoş Geldiniz ekranında veya gelen **Yönet** menüsü.
   3. Tıklatın **sonraki** başlamadan önce sayfasında.
   4. Seçin **rol tabanlı veya özellik tabanlı yükleme**ve ardından **sonraki**.
   5. Yerel makine listeden seçin ve ardından **sonraki**.
   6. Seçin **Uzak Masaüstü Hizmetleri**ve ardından **sonraki**.
   7. Genişletme **kullanıcı arabirimleri ve altyapısı** seçip **masaüstü deneyimi**.
   8. Tıklatın **Özellik Ekle**ve ardından **sonraki**.
   9. Uzak Masaüstü Hizmetleri sayfasında, tıklatın **sonraki**.
   10. Tıklatın **Uzak Masaüstü oturumu ana bilgisayarı**.
   11. Tıklatın **Özellik Ekle**ve ardından **sonraki**.
   12. Yükleme seçimlerini onaylayın sayfasında, seçin **gerekirse hedef sunucuyu otomatik olarak yeniden**ve ardından **Evet** yeniden başlatma uyarısı üzerinde.
   13. **Yükle**'ye tıklayın. Bilgisayar yeniden başlatılır.
5. .NET Framework 3.5 gibi uygulamalarınızın gerektirdiği ek özellikleri yükleyin. Özellikleri yüklemek için Ekle roller ve Özellikler Sihirbazı'nı çalıştırın.
6. Yükleyin ve programları ve RemoteApp aracılığıyla yayımlamak istediğiniz uygulamaları yapılandırın.

> [!IMPORTANT]
> Görüntü RemoteApp yüklenmeden önce uygulama uyumluluğu ile ilgili tüm sorunları bulunduğundan emin olmak için uygulamaları yüklemeden önce RDSH rolünü yükleyin.
> 
> Uygulamanıza bir kısayol emin olun (**.lnk** dosyası) görünür **Başlat** menü tüm kullanıcılar (%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs). İçinde gördüğünüz simge de emin **Başlat** menü olan kullanıcıların görmesini istediğiniz. Değilse, bunu değiştirin. (Bunu yapmanız *sahip* başlatmak için bir uygulama eklemek için menü, ancak kolaylaştırır çok Remoteapp'te uygulama yayımlama. Aksi takdirde, uygulama yayımladığınızda, yükleme yolu için uygulama girmeniz gerekir.)
> 
> 

1. Uygulamalarınızın gereksinim duyduğu ek Windows yapılandırmalara gerçekleştirin.
2. Şifreleme Dosya Sistemi (EFS) devre dışı bırakın. Bir yükseltilmiş komut penceresine aşağıdaki komutu çalıştırın:
   
     Fsutil davranışı disableencryption 1 ayarlama
   
   Alternatif olarak, ayarlama veya kayıt defterinde aşağıdaki DWORD değerini ekleyin:
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. Görüntünüzü bir Azure sanal makine içinde oluşturuluyorsa, yeniden adlandırma  **\%windir%\Panther\Unattend.xml** dosya gibi bu daha sonra çalışmasını kullanılan karşıya yükleme komut dosyası engeller. Dağıtımınızı döndürmeye gerek durumunda yine dosyayı gerekir böylece Unattend.old için bu dosya adını değiştirin.
4. Windows Update sitesine gidin ve tüm önemli güncelleştirmeleri yükleyin. Windows Update tüm güncelleştirmeleri almak için birden çok kez çalıştırmanız gerekebilir. (Bazen bir güncelleştirmeyi yüklemek ve bir güncelleştirme bu güncelleştirmeyi gerektirir.)
5. SYSPREP görüntü. Yükseltilmiş bir komut isteminde aşağıdaki komutu çalıştırın:
   
   **C:\Windows\System32\sysprep\sysprep.exe / generalize/oobe Shutdown**
   
   **Not:** kullanmayın **/mode:vm** anahtar bu sanal makine olsa bile SYSPREP komutu.

## <a name="next-steps"></a>Sonraki adımlar
Özel şablon görüntünüzü sahip olduğunuza göre RemoteApp koleksiyonunuzun bu görüntüyü karşıya gerekir. Bilgi aşağıdaki makalelerde, koleksiyonunuzu oluşturmak için kullanın:

* [RemoteApp karma koleksiyonu oluşturma](remoteapp-create-hybrid-deployment.md)
* [RemoteApp bulut koleksiyonu oluşturma](remoteapp-create-cloud-deployment.md)

