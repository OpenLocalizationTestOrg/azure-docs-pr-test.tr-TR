---
title: "Azure yük dengeleyici aaaTroubleshoot | Microsoft Docs"
description: "Azure yük dengeleyici ile ilgili bilinen sorunlar sorun giderme"
services: load-balancer
documentationcenter: na
author: RamanDhillon
manager: timlt
editor: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2017
ms.author: kumud
ms.openlocfilehash: 56b73fcbf0bbf18cedfd113a280cfafa2a3dc9f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-load-balancer"></a>Azure yük dengeleyici sorun giderme

Bu sayfa, ortak Azure yük dengeleyici sorular için sorun giderme bilgileri sağlar. Merhaba yük dengeleyiciye kullanılamadığında hello en yaygın belirtiler aşağıdaki gibidir: 
- Merhaba yük dengeleyici arkasında VM'ler toohealth yoklamaları yanıt vermiyor 
- Merhaba yük dengeleyici arkasında VM'ler hello yapılandırılan bağlantı noktasındaki toohello trafiğe yanıt vermiyor

## <a name="symptom-vms-behind-hello-load-balancer-are-not-responding-toohealth-probes"></a>Belirti: Hello yük dengeleyici arkasında VM'ler toohealth yoklamaları yanıt vermiyor
Merhaba arka uç sunucuları tooparticipate için hello yük dengeleyici kümesinde, hello araştırma onay geçmesi gerekir. Sistem durumu araştırmalarının hakkında daha fazla bilgi için bkz: [anlama yük dengeleyici yoklamaları](load-balancer-custom-probe-overview.md). 

Merhaba yük dengeleyici arka uç havuzu VM'ler yanıt toohello yoklamaları hello aşağıdaki nedenlerden biri son tooany: 
- Yük Dengeleyici arka uç havuzu VM sağlam değil 
- Yük Dengeleyici arka uç havuzu VM hello araştırma bağlantı noktasında dinleme yapmıyor 
- Güvenlik Duvarı ya da bir ağ güvenlik grubu hello yük dengeleyici arka uç havuzu VM'ler hello bağlantı noktasını engelliyor 
- Yük Dengeleyici diğer yapılandırma hataları

### <a name="cause-1-load-balancer-backend-pool-vm-is-unhealthy"></a>Neden 1: Yük dengeleyici arka uç havuzu VM sağlam değil 

**Doğrulama ve çözümleme**

tooresolve Bu sorun VM'ler katılan toohello oturum ve hello VM durumunu sistem durumunun iyi olup olmadığını denetleyin ve çok yanıtlayabilir**PsPing** veya **TCPing** hello havuzundaki başka bir VM'den. Hello VM sağlam değil veya yüklenemiyor toorespond toohello araştırma bırakılırsa, hello sorunu düzeltin ve hello VM Yük Dengeleme katılabilmesi için önce tooa sağlıklı duruma geri alın.

### <a name="cause-2-load-balancer-backend-pool-vm-is-not-listening-on-hello-probe-port"></a>Neden 2: Yük dengeleyici arka uç havuzu VM hello araştırma bağlantı noktasında dinleme yapmıyor
Merhaba VM sağlıklı olduğundan, ancak toohello araştırma yanıt vermiyor, olası bir nedeni hello sonda bağlantı noktası üzerinde VM katılan hello açık değil veya hello VM Bu bağlantı noktasında dinleme yapmıyor olabilir.

**Doğrulama ve çözümleme**

1. Toohello arka VM oturum açın. 
2. Bir komut istemi açın ve komut toovalidate hello araştırma bağlantı noktasını dinleyen bir uygulama aşağıdaki hello çalıştırın:   
            Netstat - bir
3. Başlangıç bağlantı noktası durumu olarak listelenmemişse **DİNLEME**, hello doğru bağlantı noktasını yapılandırın. 
4. Alternatif olarak, olarak listelenen başka bir bağlantı noktası seçin **DİNLEME**ve dengeleyici yapılandırması uygun şekilde yük güncelleştirme.              

###<a name="cause-3-firewall-or-a-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vms"></a>3. neden: Başlangıç bağlantı noktası hello yük dengeleyici arka uç havuzu VM'ler üzerinde güvenlik duvarı ya da bir ağ güvenlik grubu engelliyor  
Merhaba Güvenlik Duvarı'nı VM hello sonda bağlantı noktası veya hello alt ağdaki veya hello VM, yapılandırılmış bir veya daha fazla ağ güvenlik grupları engelleme hello izin vermiyor. hello araştırma tooreach hello bağlantı noktası, hello VM oluşturulamıyor toorespond toohello durumu araştırması olur.          

**Doğrulama ve çözümleme**

* Merhaba Güvenlik Duvarı etkinse, yapılandırılıp yapılandırılmadığını denetleyin tooallow hello sonda bağlantı noktası. Aksi durumda, hello güvenlik duvarı tooallow trafiği hello araştırma bağlantı noktasında yapılandırın ve yeniden sınayın. 
* Ağ güvenlik grupları Hello listeden hello araştırma bağlantı noktasında hello gelen veya giden trafiği girişim olup olmadığını denetle. 
* Ayrıca, denetleyin bir **Reddet tüm** ağ güvenlik grupları kural hello hello VM NIC üzerinde veya LB araştırmalar & trafiğine izin veren hello varsayılan kuralı daha yüksek önceliğe sahip alt hello (ağ güvenlik grupları izin vermelidir yük dengeleyici IP 168.63.129.16). 
* Bu kurallardan herhangi birinin hello araştırma trafiğini engelliyor, kaldırmak ve hello kuralları tooallow hello araştırma trafiği yeniden yapılandırın.  
* Merhaba VM şimdi toohello sistem durumu araştırmalarının yanıt başlatılmış olup olmadığını test edin. 

### <a name="cause-4-other-misconfigurations-in-load-balancer"></a>4. neden: Diğer yapılandırma hataları yük dengeleyici
Tüm Merhaba, önceki nedenler doğrulandı ve doğru şekilde çözümlenen toobe ve VM hala değil toohello durumu araştırması yanıt sonra el ile için bağlanabilirliği test edin ve bazı izlemeler toounderstand hello bağlantı toplama hello arka uç gibi görünüyor.

**Doğrulama ve çözümleme**

* Kullanım **Psping** hello birinden diğer VM'ler içinde VNet tootest hello araştırma bağlantı noktası yanıt hello (örnek:.\psping.exe -t 10.0.0.4:3389) ve sonuçları kaydedin. 
* Kullanım **TCPing** hello birinden diğer VM'ler içinde VNet tootest hello araştırma bağlantı noktası yanıt hello (örnek:.\tcping.exe 10.0.0.4 3389) ve kayıt sonuçları. 
* Yanıt bu ping testlerinde sonra alınırsa
    - Bir eş zamanlı çalıştırma Netsh trace hello hedef arka uç havuzu VM ve başka bir test VM hello aynı sanal ağ. Şimdi, belirli bir süre için PsPing testi, bazı ağ izleri toplamak ve hello testi durdurma. 
    - Hello ağ yakalama çözümlemek ve her iki gelen ve giden paketler ilgili toohello ping sorgu olup olmadığını görebilirsiniz. 
        - Hiçbir gelen paket hello arka uç havuzu VM uyulması gereken, büyük olasılıkla bir ağ güvenlik grupları veya yoktur UDR hatalı yapılandırması engelleme hello trafiği. 
        - Hiçbir giden paketlerin hello arka uç havuzu VM uyulması gereken, hello VM ilgisiz sorunları (için eample, uygulama engelleme hello sonda bağlantı noktası) için kullanıma toobe gerekir. 
    - Merhaba yük dengeleyici ulaşmadan önce Karşılama araştırma paketleri zorlanmış tooanother hedef (büyük olasılıkla ayarlarıyla UDR) yükleniyor olmadığını doğrulayın. Bu hello trafiği toonever ulaşma hello arka uç VM neden olabilir. 
* Merhaba araştırma türü (örneğin, HTTP tooTCP) değiştirin ve hello sorun araştırma yanıtı hello yapılandırmayla ise hello karşılık gelen bağlantı noktası ACL'leri ağ güvenlik gruplarındaki ve güvenlik duvarı toovalidate yapılandırın. Sistem durumu araştırma yapılandırması hakkında daha fazla bilgi için bkz: [Yük Dengeleme uç noktası sistem durumu araştırma Yapılandırması](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/).

## <a name="symptom-vms-behind-load-balancer-are-not-responding-tootraffic-on-hello-configured-data-port"></a>Belirti: Yük dengeleyicinin arkasındaki VM'ler tootraffic yapılandırılmış hello veri bağlantı noktası üzerinde yanıt vermiyor

Bir arka uç havuzu VM sağlıklı olarak listelenir ve toohello sistem durumu araştırmalarının yanıt verir ancak hala hello Yük Dengeleme katılmıyor veya toohello veri trafiği yanıt vermiyor, son olabilir nedenleri aşağıdaki hello tooany: 
* Yük Dengeleyici arka uç havuzu VM hello veri bağlantı noktasında dinleme yapmıyor 
* Ağ güvenlik grubu hello yük dengeleyici arka uç havuzu VM hello bağlantı noktası engelleme  
* Merhaba erişme yük Dengeleyiciden hello aynı VM ve NIC 
* Yük Dengeleyici arka uç havuzu VM katılan hello Hello Internet yük dengeleyici VIP erişme 

### <a name="cause-1-load-balancer-backend-pool-vm-is-not-listening-on-hello-data-port"></a>1. neden: Yük dengeleyici arka uç havuzu VM hello veri bağlantı noktasında dinleme değil 
Bir VM toohello veri trafiği yanıt vermiyorsa hello hedef bağlantı noktası üzerinde VM katılan hello açık değil veya hello VM Bu bağlantı noktasında dinleme yapmıyor olmadığından olabilir. 

**Doğrulama ve çözümleme**

1. Toohello arka VM oturum açın. 
2. Bir komut istemi açın ve komut toovalidate hello veri bağlantı noktasını dinleyen bir uygulama aşağıdaki hello çalıştırın:  
            Netstat - bir 
3. Başlangıç bağlantı noktası durumuyla listelenmemişse "DİNLEME" Merhaba uygun dinleyicisi bağlantı noktası yapılandırın 
4. Merhaba bağlantı noktasını dinleme olarak işaretlenmişse, olası sorunlar için bu bağlantı noktasında hello hedef uygulama denetleyin. 

### <a name="cause-2-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vm"></a>Neden 2: Başlangıç bağlantı noktası hello yük dengeleyici arka uç havuzu VM üzerinde ağ güvenlik grubu engelliyor  

Bir veya daha fazla ağ güvenlik grubu hello alt ağdaki veya hello VM üzerinde yapılandırılmış, hello VM oluşturulamıyor toorespond sonra hello kaynak IP veya bağlantı noktası, engelliyor.

* Merhaba arka uç VM yapılandırılmış hello ağ güvenlik grupları listesi. Daha fazla bilgi için bkz.
    -  [Ağ güvenlik grupları Hello Portal kullanarak yönetme](../virtual-network/virtual-network-manage-nsg-arm-portal.md)
    -  [PowerShell’i kullanarak ağ güvenlik gruplarını yönetme](../virtual-network/virtual-network-manage-nsg-arm-ps.md)
* Ağ güvenlik grupları Hello listeden kontrol edin:
    - Merhaba gelen veya giden trafiği hello veri noktasında girişim sahiptir. 
    - bir **Reddet tüm** ağ güvenlik grubu kural hello NIC, yük dengeleyici araştırmalar ve trafiğine izin veren bu hello varsayılan kural yüksek önceliği olan hello VM veya hello alt ağının üzerinde (ağ güvenlik grupları izin vermelidir yük dengeleyici IP Sonda bağlantı noktası olan 168.63.129.16) 
* Merhaba kurallardan herhangi birinin hello trafiğini engelliyor, kaldırın ve bu kuralları tooallow hello veri trafiği yeniden yapılandırın.  
* Merhaba VM şimdi toorespond toohello sistem durumu araştırmalarının başlatılmış olup olmadığını test edin.

### <a name="cause-3-accessing-hello-load-balancer-from-hello-same-vm-and-network-interface"></a>3. neden: Hello yük dengeleyici hello erişme aynı VM ve ağ arabirimi 

Uygulamanızı Hello arka VM yük dengeleyicinin barındırılan başka bir uygulama içinde barındırılan tooaccess çalışırsa hello aynı arka VM hello üzerinden aynı ağ arabirimi, desteklenmeyen bir senaryodur ve başarısız olur. 

**Çözümleme** yöntemler aşağıdaki hello biri aracılığıyla bu sorunu çözümlemek için:
* Uygulama başına sanal makineleri ayrı arka uç havuzunu yapılandırın. 
* Her uygulamanın kendi ağ arabirimi ve IP adresi kullanarak şekilde hello uygulama ikili NIC Vm'lerde yapılandırın. 

### <a name="cause-4-accessing-hello-internal-load-balancer-vip-from-hello-participating-load-balancer-backend-pool-vm"></a>4. neden: hello iç yük dengeleyici VIP yük dengeleyici arka uç havuzu VM katılan hello erişme

Bir sanal ağ içinde bir ILB VIP yapılandırılmışsa ve hello katılımcı arka uç VM'ler biri çalışıyor tooaccess hatası sonucu iç yük dengeleyici VIP, hello. Bu senaryo desteklenmez.
**Çözümleme** değerlendirmek uygulama ağ geçidi veya diğer proxy'leri (örneğin, nginx veya haproxy) toosupport senaryo bu tür. Uygulama ağ geçidi hakkında daha fazla bilgi için bkz: [Application Gateway genel bakış](../application-gateway/application-gateway-introduction.md)

## <a name="additional-network-captures"></a>Ek ağ yakalamaları
Bir destek servis talebi tooopen karar verirseniz, daha hızlı bir çözüm için bilgileri aşağıdaki hello toplayın. Testler aşağıdaki tek arka uç VM tooperform hello seçin:
- Merhaba VNet tootest hello araştırma bağlantı noktası yanıt içinde hello arka uç VM'ler birinden Psping kullanın (örnek: psping 10.0.0.4:3389) ve sonuçları kaydedin. 
- Merhaba VNet tootest hello araştırma bağlantı noktası yanıt içinde hello arka uç VM'ler birinden TCPing kullanın (örnek: psping 10.0.0.4:3389) ve sonuçları kaydedin.
- Bu ping testlerinde yanıt alınmazsa, eşzamanlı Netsh trace hello arka uç VM çalıştırın ve PsPing çalıştırın, ardından hello Netsh izleme durdurma sırada VNet test VM hello. 
  
## <a name="next-steps"></a>Sonraki adımlar

Merhaba önceki adımları hello sorunu çözmezse, açık bir [destek bileti](https://azure.microsoft.com/support/options/).

