---
title: "aaaAzure VMware tooAzure Site kurtarma sorunlarını giderme | Microsoft Docs"
description: "Azure sanal makineleri çoğaltırken hatalarında sorun giderme"
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Mobilite hizmetinin göndermeli yükleme sorunlarını giderme

Bu makalede hello sık karşılaşılan sorunları tooinstall hello Mobility hizmeti korumasını etkinleştirmek için toosource sunucuda çalışırken karşılaştığı ayrıntılarını verir.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(Hata kodu 95107) Koruma etkinleştirilemedi.
**Hata kodu** | **Olası nedenler** | **Hata özel öneriler**
--- | --- | ---
95107 </br>***İleti -*** hello mobility hizmeti toohello kaynak makineye göndererek yüklenmesi hata koduyla başarısız oldu ***EP0858***. <br> Sağlanan tooinstall mobility hizmeti hello kimlik bilgileri yanlış veya hello kullanıcı hesabı yetersiz ayrıcalıklara sahip | Kullanıcı kimlik bilgilerini tooinstall mobility hizmeti kaynak makinede yanlış sağlanır | Yapılandırma sunucusundaki hello kaynak makine için sağlanan hello kullanıcı kimlik bilgilerinin doğru olduğundan emin olun. <br> Kullanıcı kimlik bilgilerini tooadd/Düzenle: gidin tooconfiguration server > Cspsconfigtool simgesi > hesabını yönetin. </br> Ayrıca, olun ön koşullar altında olan checked toosuccessfully tam yükleme.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(Hata kodu 95015) Koruma etkinleştirilemedi.
**Hata kodu** | **Olası nedenler** | **Hata özel öneriler**
--- | --- | ---
95105 </br>***İleti -*** hello mobility hizmeti toohello kaynak makineye göndererek yüklenmesi hata koduyla başarısız oldu ***EP0856***. <br> "Dosya ve Yazıcı Paylaşımı" Merhaba kaynak makinede izin verilmiyor veya hello işlem sunucusu ve hello kaynak makine arasında ağ bağlantısı sorunları vardır| Dosya ve yazıcı paylaşımını etkin değil | "Dosya ve Yazıcı Paylaşımı" Merhaba kaynak makinede hello Windows Güvenlik Duvarı, Git toohello kaynak makine izin > altında Windows Güvenlik Duvarı ayarlarını > "bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin ver" > "Dosya ve yazıcı paylaşımı tüm profiller için" seçin. </br> Ayrıca, olun ön koşullar altında olan checked toosuccessfully tam yükleme.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(Hata kodu 95117) Koruma etkinleştirilemedi.
**Hata kodu** | **Olası nedenler** | **Hata özel öneriler**
--- | --- | ---
95117 </br>***İleti -*** hello mobility hizmeti toohello kaynak makineye göndererek yüklenmesi hata koduyla başarısız oldu ***EP0865***. <br> Merhaba kaynak makine çalışmıyor veya hello işlem sunucusu ve hello kaynak makine arasında ağ bağlantısı sorunları vardır | İşlem sunucusu ve kaynak sunucusu arasında ağ bağlantısı | İşlem sunucusu ve kaynak sunucu arasındaki bağlantıyı denetleyin. </br> Ayrıca, olun ön koşullar altında olan checked toosuccessfully tam yükleme.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(Hata kodu 95103) Koruma etkinleştirilemedi.
**Hata kodu** | **Olası nedenler** | **Hata özel öneriler**
--- | --- | ---
95103 </br>***İleti -*** hello mobility hizmeti toohello kaynak makineye göndererek yüklenmesi hata koduyla başarısız oldu ***EP0854***. <br> "Windows Yönetim Araçları (WMI)" Merhaba kaynak makinede izin verilmiyor veya hello işlem sunucusu ve hello kaynak makine arasında ağ bağlantısı sorunları vardır| Windows Yönetim Araçları (WMI) hello Windows Güvenlik Duvarı engellendi | Windows Yönetim Araçları (WMI) hello Windows Güvenlik Duvarı'nı verin. Windows Güvenlik Duvarı ayarları altında > "bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin ver" > "Tüm profiller için WMI Seç". </br> Ayrıca, olun ön koşullar altında olan checked toosuccessfully tam yükleme.

## <a name="check-push-install-logs-for-errors"></a>Yükleme günlükleri gönderme hata olup olmadığını denetleyin

'PushinstallService' bulunan toofile Hello yapılandırma/işlem sunucusunda gidin <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand hello kaynağı hello sorun ve aşağıdaki adımları tooresolve hello sorun giderme amacıyla kullanın.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Windows için anında yükleme ön koşullar
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>"Dosya ve Yazıcı Paylaşımı" etkinleştirildiğinden emin olun
"Dosya ve Yazıcı Paylaşımı" ve "Windows Yönetim Araçları" Merhaba kaynak makinede hello Windows Güvenlik Duvarı izin ver </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Kaynak makine etki alanına katılmış ise: </br>
Grup İlkesi Yönetim Konsolu (GPMC) kullanarak güvenlik duvarı ayarlarını yapılandırın.
1. Oturum açma tooActive directory etki alanı yöneticisi olarak makine ve Grup İlkesi Yönetim Konsolu'nu (GPMC. açın Bir çalıştırın MSC > çalıştırın).</br>
3. GPMC yüklü değilse hello çok bağlantıyı[yükleme hello GPMC](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. Merhaba GPMC konsol ağacında, Grup İlkesi nesneleri hello orman ve etki alanı çift tıklatın ve çok gidin "Varsayılan etki alanı ilkesi". </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. "Varsayılan etki alanı ilkesi üzerinde" sağ tıklayın > Düzenle > Yeni bir "Grup İlkesi Yönetimi Düzenleyicisi" penceresi açılır. </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. Merhaba Grup İlkesi Yönetimi Düzenleyicisi tooComputer yapılandırma gidin > ilkeler > Yönetim Şablonları > Ağ > ağ bağlantıları > Windows Güvenlik Duvarı. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Etki alanı profili ve standart profil ayarlarını aşağıdaki hello etkinleştir </br>
a) özel durum çift "Windows Güvenlik Duvarı: gelen dosya ve Yazıcı Paylaşımı özel durumuna izin ver". Etkin seçin ve Tamam'ı tıklatın. </br>
b) çift özel tıklayın "Windows Güvenlik Duvarı: gelen uzaktan yönetim özel durumuna izin ver". Etkin seçin ve Tamam'ı tıklatın. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Kaynak makine etki alanına katılmış ve çalışma grubunun parçası değilse </br>
Uzak makinede (çalışma grubu için) güvenlik duvarı ayarlarını yapılandırın:
1. Toohello kaynak makine gidin,</br>
2. Windows Güvenlik Duvarı ayarları altında > "bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin ver" > "Dosya ve yazıcı paylaşımı tüm profiller için" seçin. </br>
3. Windows Güvenlik Duvarı ayarları altında > "bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin ver" > "Tüm profiller için WMI Seç". </br>

#### <a name="disable-remote-user-account-control-uac"></a>Uzak kullanıcı hesabı denetimi (UAC) devre dışı bırak
Kayıt defteri anahtarı toopush hello mobility hizmetini kullanarak UAC devre dışı bırakın.
1. Başlat'a tıklayın > Çalıştır > regedit yazın > girin
2. Bulun ve aşağıdaki kayıt defteri alt anahtarı hello tıklatın: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. Merhaba LocalAccountTokenFilterPolicy kayıt defteri girdisini mevcut değilse, aşağıdaki adımları izleyin:
4. Merhaba Düzen menüsünde > Yeni > DWORD değerini tıklatın.
5. LocalAccountTokenFilterPolicy yazın ve ENTER tuşuna basın.
6. LocalAccountTokenFilterPolicy sağ tıklayın ve ardından Değiştir'i tıklatın.
7. Merhaba değer verisi kutusundaki 1 yazın ve ardından Tamam'ı tıklatın.
8. Çıkış Kayıt Defteri Düzenleyicisi.


## <a name="push-install-pre-requisites-for-linux"></a>Linux için anında yükleme ön koşullar:

1. Kök kullanıcı hello kaynak Linux sunucuda oluşturun. (Yalnızca hello anında yükleme ve güncelleştirmeleri için bu hesabı kullanın)</br>
2. Merhaba kaynak sunucu tüm ağ bağdaştırıcıları ile ilişkili hello yerel ana bilgisayar adı tooIP adresleri eşleyin girişlerine sahip Linux bu hello/etc/hosts dosyasını denetleyin. </br>
3. Merhaba son openssh, openssh sunuculu ve openssl paketleri kaynak Linux sunucusu üzerinde yüklü olduğundan emin olun. </br>
SSH bağlantı noktası 22 etkin ve çalışır durumda olduğunu denetleyin. </br>
4. Eski girişleri aracıların zaten hello kaynak sunucuda mevcut olup olmadığını hello eski aracılarını kaldırmak denetleyin ve hello sunucuyu yeniden başlatın, aracıyı yeniden yükleyin. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>SFTP alt sistemi ve parola kimlik doğrulaması hello sshd_config dosyasında etkinleştir
1. Kaynak sunucuda kök olarak oturum açın. </br>
2. Merhaba dosya /etc/ssh/sshd_config dosyasında</br> PasswordAuthentication ile başlayan hello satırını bulun. </br>
3. d.   Merhaba satırı açıklamadan çıkarın ve "Hayır" Merhaba değerinden çok "Evet" değiştirin. </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. "Alt" ile başlayan hello satırı bulun ve hello satırı açıklamadan çıkarın. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Merhaba değişiklikleri kaydedin ve hello sshd hizmetini yeniden başlatın. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>Yapılandırma/işlem sunucusu üzerinde yükleme denetimleri iletin.
#### <a name="validate-credentials-for-discovery-and-installation"></a>Bulma ve yükleme için kimlik bilgilerini doğrula

1. Yapılandırma sunucusundan Cspsconfigtool başlatma</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Koruma için kullanılan hello hesabı hello kaynak makinede yönetici haklarına sahip olduğundan emin olun. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>İşlem sunucusu ve kaynak sunucu arasındaki bağlantıyı denetleyin
1. İşlem sunucusu internet bağlantısı olduğundan emin olun.
2. WMI bağlantısı WBEMTest.exe kullanarak doğrulayın. </br>
Merhaba işlem sunucusunda, Başlat'a tıklayın > Çalıştır > wbemtest.exe > gösterildiği gibi Windows Yönetim Araçları Sınayıcısı penceresi açılacak.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Bağlan'a tıklayın > merhaba kaynak sunucu IP hello Namespace giriş kullanıcı adı ve parola girin (kaynak makine etki alanına katılmış ise, kullanıcı adı "Etkialanıadı\kullanıcıadı" olarak birlikte hello etki alanı adını belirtin. Yalnızca hello kullanıcı adını belirtin. kaynak makine çalışma grubundaysa) Merhaba kimlik doğrulama düzeyi paket gizliliği seçin. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Bağlan'ı tıklatın. Şimdi veri sağlanan hello ile Merhaba WMI bağlantısı başarılı olması gerekir ve hello Windows Yönetim Araçları Sınayıcısı penceresi aşağıda gösterildiği gibi görüntülenmesi gerekir: </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   WMI bağlantısı başarılı olmazsa olacaktır bir hata iletisi açılır. ekran görüntüsü aşağıda Hello WMI/uzaktan yönetim uygulaması izin verilen Windows Güvenlik Duvarı'nda etkin değil, başarısız bir girişim gösterir. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Merhaba WMI durumunu ve bağlantısını denetleyin.</br>
Merhaba yapılandırma/işlem sunucusunda </br>
Başlat'a tıklayın > Çalıştır > wmımgmt.msc > Eylemler > Diğer Eylemler > tooanother bilgisayarı (kaynak makine) bağlayın. </br>
Merhaba bağlantı ince ise koruması ve denetimi için kullanılan hello hesabının kimlik bilgilerini girin. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Kaynak makinenin ağ paylaşılan klasörlerine işlem sunucusu (uzaktan belirtilen kimlik bilgilerini kullanarak PS gelen) erişilebilir olduğunu doğrulayın.
  1. Oturum açma tooProcess sunucu (PS) makine, açık dosya Gezgini > merhaba adres çubuğunda şunu yazın > "\\\source-machine-ip\C$" > giriş'i tıklatın. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. Dosya Gezgini için kimlik bilgilerini ister. Merhaba kullanıcı adı ve parola girin > Tamam'ı tıklatın.</br>
   Kaynak makine etki alanına katılmış ise, kullanıcı adı ile birlikte hello etki alanı adını "Etkialanıadı\kullanıcıadı" belirtin.</br>
   Kaynak makine çalışma grubundaysa, yalnızca hello "username" sağlar. </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Bağlantı başarılı olursa, kaynak makine uzaktan gelen işlem sunucusu (PS) hello klasörleri görüntüleyebilirsiniz </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Bağlantı başarısız olursa, lütfen tüm önkoşulların yerine getirilmesini olup olmadığını denetleyin.
>

"Windows Yönetim Araçları" tooopen istemiyorsanız, ayrıca mobility hizmeti el ile Merhaba kaynak makinede yükleyebilirsiniz.</br> [Mobility hizmeti GUI aracılığıyla el ile yükleyin](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Yapılandırma Yöneticisi Kılavuzu üzerinden yükleme](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Sonraki adımlar
- [VMware sanal makineler için çoğaltmayı etkinleştirme](vmware-walkthrough-enable-replication.md)
