---
title: "Azure Site Recovery VMware Azure'a sorunlarını giderme | Microsoft Docs"
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
ms.openlocfilehash: 1e2452ccc6d3f1859a39e1ee09cdde32f53767ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Mobilite hizmetinin göndermeli yükleme sorunlarını giderme

Bu makale korumasını etkinleştirmek için kaynak sunucu Mobility hizmetini yüklemeye çalışırken karşılaştığı yaygın sorunlar ayrıntıları.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(Hata kodu 95107) Koruma etkinleştirilemedi.
**Hata kodu** | **Olası nedenler** | **Hata özel öneriler**
--- | --- | ---
95107 </br>***İleti -*** kaynak makinedeki mobilite hizmetinin göndermeli yüklemesi hata koduyla başarısız oldu ***EP0858***. <br> Mobilite hizmetinin yüklenmesi için sağlanan kimlik bilgileri yanlış veya kullanıcı hesabı yetersiz ayrıcalıklara sahip | Kaynak makinede mobilite hizmetinin yüklenmesi için sağlanan kullanıcı kimlik bilgileri yanlışsa | Yapılandırma sunucusundaki kaynak makine için sağlanan kullanıcı kimlik bilgilerinin doğru olduğundan emin olun. <br> Kullanıcı kimlik bilgilerini eklemek/düzenlemek için: yapılandırma sunucusu gidin > Cspsconfigtool simgesi > hesabını yönetin. </br> Ayrıca, aşağıda olun ön koşullar başarıyla tamamlanması göndermeli yüklemesi için denetlenir.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(Hata kodu 95015) Koruma etkinleştirilemedi.
**Hata kodu** | **Olası nedenler** | **Hata özel öneriler**
--- | --- | ---
95105 </br>***İleti -*** kaynak makinedeki mobilite hizmetinin göndermeli yüklemesi hata koduyla başarısız oldu ***EP0856***. <br> "Dosya ve Yazıcı Paylaşımı" kaynak makinede izin verilmiyor veya işlem sunucusu ve kaynak makine arasında ağ bağlantısı sorunları vardır| Dosya ve yazıcı paylaşımını etkin değil | Kaynak makineye izin ver "Dosya ve Yazıcı Paylaşımı" kaynak makinede Windows Güvenlik Duvarı'nda, Git > altında Windows Güvenlik Duvarı ayarlarını > "bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin ver" > "Dosya ve yazıcı paylaşımı tüm profiller için" seçin. </br> Ayrıca, aşağıda olun ön koşullar başarıyla tamamlanması göndermeli yüklemesi için denetlenir.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(Hata kodu 95117) Koruma etkinleştirilemedi.
**Hata kodu** | **Olası nedenler** | **Hata özel öneriler**
--- | --- | ---
95117 </br>***İleti -*** kaynak makinedeki mobilite hizmetinin göndermeli yüklemesi hata koduyla başarısız oldu ***EP0865***. <br> Kaynak makine çalışmıyor veya işlem sunucusu ve kaynak makine arasında ağ bağlantısı sorunları vardır | İşlem sunucusu ve kaynak sunucusu arasında ağ bağlantısı | İşlem sunucusu ve kaynak sunucu arasındaki bağlantıyı denetleyin. </br> Ayrıca, aşağıda olun ön koşullar başarıyla tamamlanması göndermeli yüklemesi için denetlenir.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(Hata kodu 95103) Koruma etkinleştirilemedi.
**Hata kodu** | **Olası nedenler** | **Hata özel öneriler**
--- | --- | ---
95103 </br>***İleti -*** kaynak makinedeki mobilite hizmetinin göndermeli yüklemesi hata koduyla başarısız oldu ***EP0854***. <br> "Windows Yönetim Araçları (WMI)" kaynak makinede izin verilmiyor veya işlem sunucusu ve kaynak makine arasında ağ bağlantısı sorunları vardır| Windows Yönetim Araçları (WMI) Windows Güvenlik Duvarı'nda engellendi | Windows Yönetim Araçları (WMI), Windows Güvenlik Duvarı'nda izin verin. Windows Güvenlik Duvarı ayarları altında > "bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin ver" > "Tüm profiller için WMI Seç". </br> Ayrıca, aşağıda olun ön koşullar başarıyla tamamlanması göndermeli yüklemesi için denetlenir.

## <a name="check-push-install-logs-for-errors"></a>Yükleme günlükleri gönderme hata olup olmadığını denetleyin

Yapılandırma/işlem sunucusunda bulunan 'PushinstallService' dosyasına gidin <Microsoft Azure Site Recovery Install Location>sorunun kaynağını anlamak ve sorunu çözmek için sorun giderme adımları aşağıda kullanmak için \home\svsystems\pushinstallsvc\.</br>
![pushiinstalllogs](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Windows için anında yükleme ön koşullar
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>"Dosya ve Yazıcı Paylaşımı" etkinleştirildiğinden emin olun
"Dosya ve Yazıcı Paylaşımı" ve "Windows Yönetim Araçları" Windows Güvenlik Duvarı'nda Kaynak makinede izin ver </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Kaynak makine etki alanına katılmış ise: </br>
Grup İlkesi Yönetim Konsolu (GPMC) kullanarak güvenlik duvarı ayarlarını yapılandırın.
1. Active directory etki alanı makine açık Grup İlkesi Yönetim Konsolu (GPMC yönetici olarak oturum açın. Bir çalıştırın MSC > çalıştırın).</br>
3. GPMC yüklü değilse, bağlantıyı [GPMC yükleme](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. GPMC konsol ağacında orman ve etki alanı Grup İlkesi nesneleri çift tıklatın ve "Etki alanı ilkesi varsayılan" gidin. </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. "Varsayılan etki alanı ilkesi üzerinde" sağ tıklayın > Düzenle > Yeni bir "Grup İlkesi Yönetimi Düzenleyicisi" penceresi açılır. </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. Grup İlkesi Yönetimi Düzenleyicisi'nde gidin bilgisayar yapılandırması > ilkeler > Yönetim Şablonları > Ağ > ağ bağlantıları > Windows Güvenlik Duvarı. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Etki alanı profili ve standart profili için aşağıdaki ayarları etkinleştirin </br>
a) özel durum çift "Windows Güvenlik Duvarı: gelen dosya ve Yazıcı Paylaşımı özel durumuna izin ver". Etkin seçin ve Tamam'ı tıklatın. </br>
b) çift özel tıklayın "Windows Güvenlik Duvarı: gelen uzaktan yönetim özel durumuna izin ver". Etkin seçin ve Tamam'ı tıklatın. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Kaynak makine etki alanına katılmış ve çalışma grubunun parçası değilse </br>
Uzak makinede (çalışma grubu için) güvenlik duvarı ayarlarını yapılandırın:
1. Kaynak makineye gidin,</br>
2. Windows Güvenlik Duvarı ayarları altında > "bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin ver" > "Dosya ve yazıcı paylaşımı tüm profiller için" seçin. </br>
3. Windows Güvenlik Duvarı ayarları altında > "bir uygulama veya özelliğin güvenlik duvarı aracılığıyla izin ver" > "Tüm profiller için WMI Seç". </br>

#### <a name="disable-remote-user-account-control-uac"></a>Uzak kullanıcı hesabı denetimi (UAC) devre dışı bırak
Mobility hizmetinin gönderim için kayıt defteri anahtarını kullanarak UAC devre dışı bırakın.
1. Başlat'a tıklayın > Çalıştır > regedit yazın > girin
2. Bulun ve ardından aşağıdaki kayıt defteri alt anahtarı: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. LocalAccountTokenFilterPolicy kayıt defteri girdisini mevcut değilse, aşağıdaki adımları izleyin:
4. Düzen menüsünde > Yeni > DWORD değerini tıklatın.
5. LocalAccountTokenFilterPolicy yazın ve ENTER tuşuna basın.
6. LocalAccountTokenFilterPolicy sağ tıklayın ve ardından Değiştir'i tıklatın.
7. Değer verisi kutusundaki 1 yazın ve ardından Tamam'ı tıklatın.
8. Çıkış Kayıt Defteri Düzenleyicisi.


## <a name="push-install-pre-requisites-for-linux"></a>Linux için anında yükleme ön koşullar:

1. Kök kullanıcı kaynak Linux sunucuda oluşturun. (Yalnızca anında yükleme ve güncelleştirmeleri için bu hesabı kullanın)</br>
2. Kaynak Linux sunucusundaki /etc/hosts dosyasında, yerel ana bilgisayar adını tüm ağ bağdaştırıcıları ile ilişkili IP adreslerine eşleyen girişler olduğunu denetleyin. </br>
3. En son openssh, openssh sunuculu ve openssl paketlerin kaynak Linux sunucusu üzerinde yüklü olduğundan emin olun. </br>
SSH bağlantı noktası 22 etkin ve çalışır durumda olduğunu denetleyin. </br>
4. Eski girişleri aracıların zaten kaynak sunucuda mevcut olup olmadığını eski aracıları kaldırın denetleyin ve sunucuyu yeniden başlatın, aracıyı yeniden yükleyin. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-the-sshdconfig-file"></a>SFTP alt sistemi ve parola kimlik doğrulaması sshd_config dosyasında etkinleştir
1. Kaynak sunucuda kök olarak oturum açın. </br>
2. Dosya /etc/ssh/sshd_config dosyasında</br> PasswordAuthentication ile başlayan satırı bulun. </br>
3. d.   Satırı açıklamadan çıkarın ve "Evet" için "Hayır" değerini değiştirin. </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. "Alt" ile başlayan satırı bulun ve satırı açıklamadan çıkarın. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Değişiklikleri kaydetmek ve sshd hizmetini yeniden başlatın. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>Yapılandırma/işlem sunucusu üzerinde yükleme denetimleri iletin.
#### <a name="validate-credentials-for-discovery-and-installation"></a>Bulma ve yükleme için kimlik bilgilerini doğrula

1. Yapılandırma sunucusundan Cspsconfigtool başlatma</br>
![WMItestConnect5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Koruma için kullanılan hesap kaynak makinede yönetici haklarına sahip olduğundan emin olun. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>İşlem sunucusu ve kaynak sunucu arasındaki bağlantıyı denetleyin
1. İşlem sunucusu internet bağlantısı olduğundan emin olun.
2. WMI bağlantısı WBEMTest.exe kullanarak doğrulayın. </br>
İşlem sunucusundaki, Başlat'a tıklayın > Çalıştır > wbemtest.exe > gösterildiği gibi Windows Yönetim Araçları Sınayıcısı penceresi açılacak.</br>
   ![WMItestConnect1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Bağlan'a tıklayın > kaynak sunucu IP'si Namespace giriş kullanıcı adını ve parolayı girin (kaynak makine etki alanına katılmış ise, kullanıcı adı "Etkialanıadı\kullanıcıadı" olarak birlikte etki alanı adını belirtin. Yalnızca kullanıcı adını belirtin. kaynak makine çalışma grubundaysa) Kimlik doğrulama düzeyi paket gizliliği seçin. </br>
![WMItestConnect2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Bağlan'ı tıklatın. Şimdi WMI bağlantısı ile sağlanan veri başarılı olması gerekir ve Windows Yönetim Araçları Sınayıcısı penceresi aşağıda gösterildiği gibi görüntülenmesi gerekir: </br>
   ![WMItestConnect3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   WMI bağlantısı başarılı olmazsa olacaktır bir hata iletisi açılır. WMI/uzaktan yönetim uygulaması izin verilen Windows Güvenlik Duvarı'nda etkin değil, başarısız bir girişim ekran görüntüsü gösterilmektedir. </br>
   ![WMItestConnect4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. WMI durumunu ve bağlantısını denetleyin.</br>
Yapılandırma/işlem sunucusu </br>
Başlat'a tıklayın > Çalıştır > wmımgmt.msc > Eylemler > Diğer Eylemler > başka bir bilgisayara (kaynak makine) bağlayın. </br>
Bağlantı ince ise koruması ve denetimi için kullanılan hesabın kimlik bilgilerini girin. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Kaynak makinenin ağ paylaşılan klasörlerine işlem sunucusu (uzaktan belirtilen kimlik bilgilerini kullanarak PS gelen) erişilebilir olduğunu doğrulayın.
  1. İşlem Sunucusu (PS) makine, açık dosya Gezgini için oturum açma > Adres çubuğu yazın > "\\\source-machine-ip\C$" > giriş'i tıklatın. </br>
  ![Fileshare1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. Dosya Gezgini için kimlik bilgilerini ister. Kullanıcı adı ve parola girin > Tamam'ı tıklatın.</br>
   Kaynak makine etki alanına katılmış ise, kullanıcı adı ile birlikte etki alanı adını "Etkialanıadı\kullanıcıadı" belirtin.</br>
   Kaynak makine çalışma grubundaysa, yalnızca "username" sağlar. </br>
  ![Fileshare2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Bağlantı başarılı olursa, kaynak makine uzaktan gelen işlem sunucusu (PS) klasörleri görüntüleyebilirsiniz </br>
  ![Fileshare3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Bağlantı başarısız olursa, lütfen tüm önkoşulların yerine getirilmesini olup olmadığını denetleyin.
>

"Windows Yönetim Araçları" açmak istemiyorsanız, ayrıca mobility hizmeti el ile kaynak makinede yükleyebilirsiniz.</br> [Mobility hizmeti GUI aracılığıyla el ile yükleyin](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Yapılandırma Yöneticisi Kılavuzu üzerinden yükleme](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Sonraki adımlar
- [VMware sanal makineler için çoğaltmayı etkinleştirme](vmware-walkthrough-enable-replication.md)
