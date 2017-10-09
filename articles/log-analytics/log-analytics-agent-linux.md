---
title: "aaaConnect, Linux bilgisayarları tooOperations Yönetim Paketi (OMS) | Microsoft Docs"
description: "Bu makalede, Azure, diğer Bulut veya şirket içi tooOMS hello OMS aracısı için Linux kullanarak barındırılan tooconnect Linux bilgisayarların nasıl açıklanmaktadır."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>Linux bilgisayarları tooOperations Yönetim Paketi (OMS) bağlanma 

Microsoft Operations Management Suite (OMS) ile toplama ve hareket Linux bilgisayarları ve fiziksel sunucularda veya sanal makineleri, sanal makinelerinizde olarak şirket içi veri Merkezinize bulunan Docker gibi kapsayıcı çözümlerinden oluşturulan veriler üzerinde bir Amazon Web Hizmetleri (AWS) veya Microsoft Azure gibi bulutta barındırılan hizmet. Güncelleştirme yönetimi toomanage yazılım güncelleştirmeleri tooproactively Linux VM'ler hello ömrünü yönetmek ve değişiklik izleme, tooidentify yapılandırma değişiklikleri gibi yönetim çözümleri OMS içinde kullanılabilir de kullanabilirsiniz. 

Merhaba OMS Aracısı Linux TCP bağlantı noktası 443 giden hello OMS hizmeti ile iletişim kurar ve hello bilgisayar tooa güvenlik duvarı veya proxy sunucu toocommunicate hello Internet bağlanıyorsa, gözden [bir HTTP Proxy'si ile kullanmak için yapılandırma hello Aracısı Sunucu veya OMS ağ geçidi](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) hangi yapılandırma değişiklikleri toounderstand uygulanan toobe gerekir.  System Center 2016 - Operations Manager veya Operations Manager 2012 R2'de, hello bilgisayarla izliyorsanız çok konaklı hello OMS hizmeti toocollect verilerini ve iletme toohello hizmetlerle olabilir ve Operations Manager tarafından yine izlenmelidir.  OMS ile tümleşik bir Operations Manager yönetim grubu tarafından izlenen Linux bilgisayarlar veri kaynakları için yapılandırma almaz ve İleri hello yönetim grubu ile veri toplanır.  Merhaba OMS Aracısı, bir çalışma alanı daha yapılandırılmış tooreport toomore olamaz.  

BT güvenlik ilkeleri, ağ tooconnect toohello Internet bilgisayarları izin vermiyorsa hello Aracısı yapılandırılmış tooconnect toohello OMS ağ geçidi tooreceive yapılandırma bilgilerini kullanılabilir ve sahip olduğunuz hello çözümüne bağlı olarak toplanan verileri gönder etkin. Daha fazla bilgi ve tooconfigure, OMS Linux Aracısı toocommunicate bir OMS ağ geçidi toohello OMS hizmeti aracılığıyla nasıl görürüm adımlar [hello OMS ağ geçidi kullanarak bilgisayarları tooOMS bağlanmak](log-analytics-oms-gateway.md).  

Merhaba Aşağıdaki diyagramda hello aracıyla yönetilen Linux bilgisayarları hello yönü ve bağlantı noktaları da dahil olmak üzere OMS arasında hello bağlantı gösterilmektedir.

![OMS diyagramı ile doğrudan aracı iletişimi](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>Sistem gereksinimleri
Başlamadan önce hello önkoşulları karşılaması ayrıntıları tooverify aşağıdaki hello gözden geçirin.

### <a name="supported-linux-operating-systems"></a>Desteklenen Linux işletim sistemleri
Linux dağıtımları aşağıdaki hello resmi olarak desteklenir.  Ancak, hello OMS Aracısı Linux için listelenmeyen diğer dağıtımlar da çalıştırabilirsiniz.

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5, 6 ve 7 (x86/x64)
* Oracle Linux 5, 6 ve 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 ve 7 (x86/x64)
* Debian GNU/Linux 6, 7 ve 8 (x86/x64)
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)
* SUSE Linux Enterprise Server 11 ve 12 (x86/x64)

### <a name="network"></a>Ağ
Liste hello proxy altındaki Hello bilgi ve güvenlik duvarı yapılandırma bilgilerini Merhaba OMS ile Linux Aracısı toocommunicate gereklidir. Ağ toohello OMS hizmetinizden trafik gidendir. 

|Aracı Kaynağı| Bağlantı Noktaları |  
|------|---------|  
|*.ods.opinsights.azure.com | Bağlantı noktası 443|   
|*.oms.opinsights.azure.com | Bağlantı noktası 443|   
|*.BLOB.Core.Windows.NET/ | Bağlantı noktası 443|   
|*.azure-automation.net | Bağlantı noktası 443|  

### <a name="package-requirements"></a>Paket gereksinimleri

 **Gerekli paket**   | **Açıklama**   | **En düşük sürüm**
--------------------- | --------------------- | -------------------
Glibc | GNU C Kitaplığı   | 2.5-12 
Openssl | OpenSSL kitaplıkları | 0.9.8E veya 1.0
Curl | cURL web istemcisi | 7.15.5
Python ctypes | | 
PAM | Eklenebilir kimlik doğrulaması modülleri | 

> [!NOTE]
>  Rsyslog veya syslog ng gerekli toocollect syslog iletileri şunlardır. Red Hat Enterprise Linux, CentOS ve Oracle Linux sürümü (sysklog) 5 sürümünü Hello varsayılan syslog arka plan syslog olay toplaması için desteklenmiyor. Bu sürümü bu dağıtımları toocollect syslog verileri hello rsyslog arka plan programı yüklenmelidir ve tooreplace sysklog yapılandırılmış 

Merhaba aracı birden çok paket içerir. Merhaba yayın dosyasını içeren paketler, çalışan hello Kabuk Paketle tarafından kullanılabilen aşağıdaki hello `--extract`:

**Paket** | **Sürüm** | **Açıklama**
----------- | ----------- | --------------
omsagent | 1.4.0 | Merhaba Linux için Operations Management Suite Aracısı
omsconfig | 1.1.1 | Merhaba OMS aracısı için yapılandırma aracısı
OMI | 1.2.0 | Yönetim Altyapısı (OMI) - hafif bir CIM sunucusu açın
scx | 1.6.3 | İşletim sistemi performans ölçümleri için OMI CIM sağlayıcıları
Apache cimprov | 1.0.1 | Apache HTTP Server performansı sağlayıcısı OMI için izleme. Apache HTTP Server algılanırsa, yüklü.
MySQL cimprov | 1.0.1 | MySQL sunucusu performans sağlayıcısı OMI için izleme. MySQL/MariaDB sunucu algılanırsa, yüklü.
docker cimprov | 1.0.0 | OMI docker sağlayıcısı. Docker algılanırsa, yüklü.

### <a name="compatibility-with-system-center-operations-manager"></a>System Center Operations Manager ile uyumluluk
Merhaba OMS Aracısı Linux Aracısı ikili dosyalarının hello System Center Operations Manager Aracısı ile paylaşır. Şu anda Operations Manager tarafından yönetilen bir sistemde Linux için hello OMS Aracısı yüklerseniz, bu hello hello bilgisayar tooa daha yeni sürümü OMI ve SCX paketleri. Bu sürüm, hello OMS ve System Center 2016 - Operations Manager/Operations Manager 2012 R2 aracıları Linux için uyumlu değildir. 

> [!NOTE]
> System Center 2012 SP1 ve önceki sürümleri şu anda hello Linux için OMS Aracısı ile desteklenen veya uyumlu değildir.<br>
> Hello OMS Aracısı Linux için Operations Manager tarafından izlenen değil yüklü tooa bilgisayar ise ve ardından toomonitor hello bilgisayar Operations Manager ile istediğiniz hello değiştirmelisiniz [OMI yapılandırma](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) önceki toodiscovering hello bilgisayar. **Bu adım *değil* hello Operations Manager Aracısı Linux için OMS aracısının hello önce yüklediyseniz gerekli.**

### <a name="system-configuration-changes"></a>Sistem yapılandırması değişiklikleri
Linux paketler için OMS aracısının Hello yükledikten sonra hello aşağıdaki ek sistem genelinde yapılandırma değişiklikleri uygulanır. Bu yapıtların Hello omsagent paket kaldırıldığında kaldırılır.

* Adlı bir ayrıcalıklı olmayan kullanıcı: `omsagent` oluşturulur. Merhaba hesap hello omsagent arka plan programı çalışırken budur.
* "Ekle" sudoers dosya /etc/sudoers.d/omsagent oluşturulur. Bu, omsagent toorestart hello syslog ve omsagent Daemon yetkilendirir. Sudo "Ekle" yönergeleri sudo yüklü hello sürümünde desteklenmez, bu girişler çok/etc/sudoers yazılır.
* Değiştirilen tooforward olayları toohello Aracısı'nın bir alt Hello syslog yapılandırmadır. Merhaba daha fazla bilgi için bkz: **yapılandırma veri toplama** bölümüne bakın

### <a name="upgrade-from-a-previous-release"></a>Önceki bir sürümünden yükseltme
Bu sürümde 1.0.0-47 desteklenenden daha önceki sürümlerden yükseltin. Merhaba Hello yüklemesini gerçekleştirme `--upgrade` komutu hello aracı toohello en son sürümü tüm bileşenlerini yükseltir.

## <a name="installing-hello-agent"></a>Merhaba Aracısı yükleniyor

Bu bölümde, nasıl tooinstall hello Debian ve RPM içeren bir bunndle kullanarak Linux için OMS Aracısı bileşenlerinden her biri hello aracı için paketler açıklanmaktadır.  Doğrudan yüklenebilir veya tooretrieve hello tek paketler ayıklanır.  

Öncelikle, OMS çalışma alanı kimliği ve toohello geçerek bulabilirsiniz anahtarınızı gerekir [OMS Klasik portal](https://mms.microsoft.com).  Merhaba üzerinde **genel bakış** sayfasından hello üst menü seçin **ayarları**ve ardından çok gidin**bağlı Sources\Linux sunuculara**.  Merhaba değeri toohello sağındaki bkz **çalışma alanı kimliği** ve **birincil anahtar**.  Kopyalayın ve her ikisi de, sık kullanılan düzenleyicisine yapıştırın.    

1. Son yükleme hello [Linux (x64) için OMS aracısının](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) veya [Linux x86 için OMS aracısının](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) github'dan.  
2. SCP/sftp kullanılarak hello uygun paket (x86 veya x64) tooyour Linux bilgisayarı aktarın.
3. Hello kullanarak yükleme hello paket `--install` veya `--upgrade` bağımsız değişkeni. 

    > [!NOTE]
    > Varolan tüm paketler, ne zaman hello System Center Operations Manager Aracısı Linux için zaten yüklenmiş gibi yüklediyseniz hello kullanın `--upgrade` bağımsız değişkeni. Yükleme sırasında tooconnect tooOperations Management Suite sağlamak hello `-w <WorkspaceID>` ve `-s <Shared Key>` parametreleri.


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall ve yerleşik doğrudan
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>tooupgrade hello aracı paketi
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>tooinstall ve US Government bulutta yerleşik tooa çalışma
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>Bir HTTP proxy sunucusu veya OMS ağ geçidi ile Merhaba aracı kullanmak için yapılandırma
bir HTTP veya HTTPS proxy sunucusu veya OMS ağ geçidi toohello OMS hizmeti ile iletişim kurmasını Hello Linux için OMS aracısının destekler.  Anonim ve temel kimlik doğrulaması (kullanıcı adı/parola) desteklenir.  

### <a name="proxy-configuration"></a>Proxy yapılandırması
Merhaba proxy yapılandırma değeri sözdizimi aşağıdaki hello sahiptir:

`[protocol://][user:password@]proxyhost[:port]`

Özellik|Açıklama
-|-
Protokol|HTTP veya https
Kullanıcı|Proxy kimlik doğrulaması için isteğe bağlı kullanıcı adı
password|Proxy kimlik doğrulaması için isteğe bağlı parola
proxyhost|Adresini veya FQDN'sini hello proxy sunucu/OMS ağ geçidi
port|Merhaba proxy sunucu/OMS ağ geçidi için isteğe bağlı bağlantı noktası numarası

Örneğin, `http://user01:password@proxy01.contoso.com:8080`

Merhaba proxy sunucusu yüklemesi sırasında veya yükleme işleminden sonra hello proxy.conf yapılandırma dosyasını değiştirerek belirtilebilir.   

### <a name="specify-proxy-configuration-during-installation"></a>Yükleme sırasında proxy yapılandırmasını belirtin
Merhaba `-p` veya `--proxy` hello omsagent yükleme paketi için bağımsız değişken hello proxy yapılandırması toouse belirtir. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>Bir dosyada Hello proxy yapılandırmasını tanımlayın
Merhaba proxy yapılandırması hello dosyalarında ayarlanabilir `/etc/opt/microsoft/omsagent/proxy.conf` ve `/etc/opt/microsoft/omsagent/conf/proxy.conf `. Merhaba dosyaları doğrudan oluşturduğunuz veya düzenlediğiniz, ancak izinlerini okuma izni hello dosyalarda güncelleştirilmiş toogrant hello omiuser kullanıcı olmalıdır. Örneğin:
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>Merhaba proxy yapılandırması kaldırılıyor
tooremove önceden tanımlanmış proxy yapılandırmasını ve toodirect bağlantı geri, hello proxy.conf dosyasını kaldırın:
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Operations Management Suite ile ekleme
Bir çalışma alanı kimliği ve anahtarı hello paket yükleme sırasında sağlanan değil, hello Aracısı sonradan Operations Management Suite ile kayıtlı olması gerekir.

### <a name="onboarding-using-hello-command-line"></a>Merhaba komut satırını kullanarak ekleme
Çalışma alanınız için anahtarı ve Hello çalışma alanı kimliği sağladığını hello omsadmin.sh komutunu çalıştırın. Bu komut (sudo yükseltmesi ile) kök olarak çalıştırmanız gerekir:
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>Bir dosyayı kullanarak ekleme
1.  Merhaba dosyası oluşturma `/etc/omsagent-onboard.conf`. Merhaba dosya okunabilir ve yazılabilir bir kök olmalıdır.
`sudo vi /etc/omsagent-onboard.conf`
2.  Çalışma alanı kimliği ve paylaşılan anahtar ile Merhaba dosyasında satırlardan hello ekleyin:

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  Aşağıdaki komut tooOnboard tooOMS hello çalıştırın:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  Merhaba dosyası üzerinde başarıyla Hazırlanmanız silinir.

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>Linux tooreport tooSystem Center Operations Manager için OMS aracısının Hello etkinleştir
Linux tooreport tooa System Center Operations Manager yönetim grubu için adımları tooconfigure hello OMS aracısı aşağıdaki hello gerçekleştirin.  

1. Merhaba dosyasını düzenleyin`/etc/opt/omi/conf/omiserver.conf`
2. Bu hello satır başlayarak olun **httpsport =** hello bağlantı noktası 1270 tanımlar. Örneğin:`httpsport=1270`
3. Merhaba OMI sunucuyu yeniden başlatın:`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>Aracı günlükleri
Linux için OMS aracısının hello bulunabilir için günlükleri Hello: `/var/opt/microsoft/omsagent/<workspace id>/log/` hello omsconfig (Aracısı yapılandırması) programı bulunabilir için günlükleri hello: `/var/opt/microsoft/omsconfig/log/` (performans ölçüm verilerini sağlayan) hello OMI ve scx farklı bileşenlerin günlüklerinde bulunabilir:`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>Günlük döndürme yapılandırma ##
Merhaba günlük döndürme yapılandırması omsagent yolda bulunabilir:`/etc/logrotate.d/omsagent-<workspace id>`

Merhaba varsayılan ayarlar şunlardır: 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>Linux için Hello OMS aracısı kaldırma
Merhaba aracı paketlerini çalışan hello paket .sh dosyasıyla hello tarafından kaldırılabilir `--purge` hello bilgisayardan hello aracısı ve yapılandırmasını tamamen kaldırır bağımsız değişkeni.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>Sorun giderme

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>Sorunu: Proxy tooOMS aracılığıyla oluşturulamıyor tooconnect

#### <a name="probable-causes"></a>Olası nedenler
* onboarding işlemi sırasında belirtilen hello proxy yanlış
* Merhaba OMS hizmet uç noktaları, veri merkezinizdeki whitelistested değildir 

#### <a name="resolutions"></a>Çözümler
1. Merhaba seçeneğiyle komut aşağıdaki hello kullanarak Linux için OMS aracısının hello ile Reonboard toohello OMS hizmetine `-v` etkin. Bu ayrıntılı çıktı hello proxy toohello OMS hizmeti bağlanma hello Aracısı'nın sağlar. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Merhaba bölümüne [bir HTTP Proxy'si ile kullanmak için yapılandırma hello Aracısı server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify düzgün yapılandırılmış bir proxy sunucu üzerinden Aracısı toocommunicate hello.    
* OMS hizmet uç noktaları hello çift onay Güvenilenler listesine şunlardır:

    |Aracı Kaynağı| Bağlantı Noktaları |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Bağlantı noktası 443|   
    |*.oms.opinsights.azure.com | Bağlantı noktası 443|   
    |ods.systemcenteradvisor.com | Bağlantı noktası 443|   
    |*.BLOB.Core.Windows.NET/ | Bağlantı noktası 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>Sorun: Bir 403 hatası tooonboard çalışırken alıyorsunuz

#### <a name="probable-causes"></a>Olası nedenler
* Tarih ve saat, Linux sunucusu üzerinde yanlış 
* Çalışma alanı kimliği ve çalışma alanı anahtarı doğru değil

#### <a name="resolution"></a>Çözüm

1. Başlangıç saati hello komutu tarihi ile Linux sunucunuzda denetleyin. Başlangıç zamanı geçerli zamandan 15 dakika +/-ise ekleme başarısız olur. toocorrect Bu güncelleştirme hello tarih ve/veya saat dilimi Linux sunucunuzun. 
2. Linux için hello hello OMS Aracısı en son sürümünü yüklediğinizden emin olun.  saat eğriltme hello ekleme hatasına neden oluyorsa hello en yeni sürümü şimdi sizi bilgilendirir.
3. Doğru çalışma alanı kimliği ve çalışma alanı bu konunun önceki kısımlarında hello yükleme yönergeleri izleyerek anahtarı kullanarak Reonboard.

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>Sorun: Sağ onboarding sonra 500 ve 404 hata hello günlük dosyasına bakın
Bu OMS çalışma alanına Linux verilerin ilk karşıya yükleme sırasında oluşan bilinen bir sorundur. Bu verilerin gönderilen veya servis deneyimi olmasıyla etkilemez.

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>Sorun: Herhangi bir veri hello OMS portalında gördüğünüz değil

#### <a name="probable-causes"></a>Olası nedenler

- Onboarding toohello OMS hizmeti başarısız oldu
- Bağlantı toohello OMS hizmetine engellendi
- Linux veriler için OMS aracısının yedeklenir

#### <a name="resolutions"></a>Çözümler
1. Ekleme hello OMS hizmetine hello aşağıdaki dosya olup olmadığını kontrol ederek başarılı olup olmadığını kontrol edin:`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Hello kullanarak Reonboard `omsadmin.sh` komut satırı yönergeleri
3. Bir proxy sunucu kullanıyorsanız, daha önce sağlanan toohello proxy çözüm adımları bakın.
4. Linux için OMS aracısının Hello hello OMS hizmeti ile iletişim kuramadığında bazı durumlarda, hello aracısında 50 MB'dir sıraya alınan toohello tam arabellek boyutu verilerdir. Linux için OMS aracısının Hello hello aşağıdaki komutu çalıştırarak başlatılması: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Aracı sürümü 1.1.0-28 ve daha sonra bu sorun düzeltilmiştir.
> 