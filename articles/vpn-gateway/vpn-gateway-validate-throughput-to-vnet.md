---
title: "VPN verimlilik tooa Microsoft Azure sanal ağı doğrulama | Microsoft Docs"
description: "Merhaba bu belgenin amacı olan toohelp bir kullanıcı kendi şirket içi kaynakları tooan Azure sanal makinesi hello ağ akışından doğrulayın."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>Nasıl toovalidate VPN verimlilik tooa sanal ağ

Bir VPN gateway bağlantısı, sanal ağınız Azure içinde ve şirket içi arasında güvenli, şirket içi bağlantılar tooestablish sağlar BT altyapısı.

Bu makalede nasıl toovalidate ağ hello veri akışından kaynakları tooan Azure sanal makinesi şirket içi gösterilmektedir. Ayrıca, sorun giderme kılavuzu sağlar.

>[!NOTE]
>Bu makale tasarlanmıştır toohelp tanılamak ve ortak sorunları giderin. Bilgi, aşağıdaki hello kullanarak oluşturulamıyor toosolve hello sorun olduğunuzda [desteğine başvurun](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
>
>

## <a name="overview"></a>Genel Bakış

Merhaba VPN ağ geçidi bağlantısı hello aşağıdaki bileşenleri içerir:

- Şirket içi VPN cihazı (bir listesini görüntülemek [doğrulanan VPN cihazları)](vpn-gateway-about-vpn-devices.md#devicetable).
- Genel Internet
- Azure VPN ağ geçidi
- Azure sanal makinesi

Aşağıdaki diyagramda hello hello mantıksal bir şirket içi ağ tooan VPN aracılığıyla Azure sanal ağ bağlantısını gösterir.

![Mantıksal müşteri ağ bağlantısı tooMSFT ağ VPN kullanarak](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>Merhaba maksimum beklenen giriş/çıkış Hesapla

1.  Uygulamanızın temel üretilen iş gereksinimlerini belirleyin.
2.  Azure VPN ağ geçidi işleme sınırları belirleyin. Yardım için hello "SKU ve VPN türüne göre toplam verimliliği" bölümüne bakın [planlama ve tasarım VPN ağ geçidi için](vpn-gateway-plan-design.md).
3.  Merhaba belirlemek [Azure VM verimlilik Kılavuzu](../virtual-machines/virtual-machines-windows-sizes.md) VM boyutu.
4.  Internet servis sağlayıcısı (ISS) bant genişliğiniz belirler.
5.  Beklenen Verimlilik - en az bant genişliği (VM, ağ geçidi, ISS) hesaplamak * 0,8.

Hesaplanan verimlilik, uygulamanızın temel üretilen iş gereksinimlerini karşılamıyorsa tooincrease hello bant genişliği hello performans sorunu tanımlanan hello kaynak gerekir. bir Azure VPN ağ geçidi tooresize bkz [bir ağ geçidi SKU'su değiştirme](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku). bir sanal makine tooresize bkz [bir VM'yi yeniden boyutlandırın](../virtual-machines/virtual-machines-windows-resize-vm.md). Beklenen Internet bant genişliği yaşıyorsanız değil, ISS toocontact da isteyebilirsiniz.

## <a name="validate-network-throughput-by-using-performance-tools"></a>Performans araçları kullanarak ağ verimliliği doğrulama

Test sırasında VPN tüneli verimlilik Doygunluk doğru sonuçlar vermez gibi bu doğrulama yoğun olmayan saatlerde gerçekleştirilmesi gerekir.

Bu test için kullandığımız hello hem Windows hem de Linux üzerinde çalışır ve hem istemci hem de sunucu modları içeren iPerf aracıdır. Windows VM'ler için sınırlı too3 Gbps olur.

Bu araç tüm okuma/yazma işlemleri toodisk gerçekleştirmez. Bu yalnızca bir son toohello diğer kendinden oluşturulmuş TCP trafiği üretir. İstemci ve sunucu düğümler arasında kullanılabilir bant hello ölçer deneme bağlı olarak istatistikleri oluşturulur. İki düğüm arasında test edilirken bir hello sunucu ve istemci olarak diğer hello gibi davranır. Bu test tamamlandıktan sonra her ikisi de indirebileceğiniz ve her iki düğüm üzerinde üretilen işi hello rolleri tootest ters öneririz.

### <a name="download-iperf"></a>İPerf indirin
Karşıdan [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip). Ayrıntılar için bkz [iPerf belgelerine](https://iperf.fr/iperf-doc.php).

 >[!NOTE]
 >Bu makalede ele hello üçüncü taraf ürünler Microsoft'tan bağımsız şirketler tarafından üretilmektedir. Microsoft, zımni ya da aksi takdirde hello performans ya da bu ürünlerin hakkında hiçbir garanti vermez.
 >
 >

### <a name="run-iperf-iperf3exe"></a>Çalışma iPerf (iperf3.exe)
1. Merhaba trafiğinde (Azure VM sınama ortak IP adresi) izin veren bir NSG/ACL kuralı etkinleştirin.

2. Her iki düğüm üzerinde 5001 bağlantı noktası için güvenlik duvarı özel durumunu etkinleştirin.

    **Windows:** yönetici olarak çalıştır hello şu komutu:

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    test ederken tooremove hello kural bu komutu çalıştırmak, tamamlanır:

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Azure Linux:** Azure Linux görüntüleri olan izin veren güvenlik duvarları. Bir bağlantı noktasını dinleyen bir uygulama olup olmadığını hello trafiğinin aracılığıyla izin verilir. Güvenli hale getirilen özel resimler açıkça açılan bağlantı noktaları gerekebilir. Ortak Linux işletim sistemi katmanlı güvenlik duvarları içeren `iptables`, `ufw`, veya `firewalld`.

3. Merhaba sunucu düğümünde iperf3.exe ayıkladığınız toohello dizini değiştirin. Ardından iPerf sunucu modunda çalıştırın ve toolisten 5001 bağlantı noktasında komutları aşağıdaki hello ayarlayın:

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. Merhaba istemci düğümde burada iperf aracı ayıkladığınız ve hello aşağıdaki komutu çalıştırın toohello dizini değiştirin:

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    Merhaba istemci bağlantı noktası 5001 toohello sunucuda trafiği 30 saniye inducing. Merhaba bayrağı '-P ' 32 eşzamanlı bağlantı toohello sunucu düğümünü kullanarak size gösterir.

    Merhaba aşağıdaki ekran bu örneğin hello çıktısını gösterir:

    ![Çıktı](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. (İsteğe bağlı) toopreserve hello sınama sonuçları, bu komutu çalıştırın:

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. Merhaba sunucu düğümü şimdi hello istemci ve tam tersini böylece hello önceki adımları tamamladıktan sonra hello rolleri ile aynı adımları tersine, hello yürütün.

## <a name="address-slow-file-copy-issues"></a>Yavaş dosya kopyalama sorunlarını gidermek
Windows Gezgini'ni kullanarak veya sürükleyip bir RDP oturumu aracılığıyla zaman kopyalamayı yavaş dosya karşılaşabilirsiniz. Bu sorun normalde tooone veya her ikisini Etkenler aşağıdaki hello oluşur:

- Dosya kopyalama uygulamaları, Windows Gezgini ve RDP, gibi birden çok iş parçacığı dosya kopyalarken kullanmayın. Çok iş parçacıklı dosya kopyalama uygulaması gibi daha iyi performans için kullandığınız [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy dosyaları 16 veya 32 iş parçacığı kullanarak. toochange hello iş parçacığı numarasını Richcopy, dosya kopyalama için tıklatın **eylem** > **kopyalama seçenekleri** > **dosya kopyalama**.<br><br>
![Yavaş dosya kopyalama sorunları](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- Yetersiz VM disk okuma/yazma hızı. Daha fazla bilgi için bkz: [Azure Storage sorunlarını giderme](../storage/common/storage-e2e-troubleshooting.md).

## <a name="on-premises-device-external-facing-interface"></a>Şirket içi cihaz dış karşılıklı arabirimi
Merhaba içi bağlı VPN cihazı Internet'e yönelik IP adresi hello dahil değilse [yerel ağ](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) tanımı azure'da hello durumlarıyla VPN bağlantısını keser veya performans sorunları yaşamaktadır toobring karşılaşabilirsiniz.

## <a name="checking-latency"></a>Gecikme olmadığı denetleniyor
Atlama arasında 100 ms aşan gecikmeleri varsa tracert tootrace tooMicrosoft Azure kenar aygıt toodetermine kullanın.

Merhaba şirket içi ağ üzerinden çalıştırılabilecek *tracert* toohello VIP hello Azure ağ geçidi ya da VM. Yalnızca gördüğünüzde * döndürülen hello Azure kenar ulaştı, biliyor. "Döndürülen MSN" içeren DNS adları gördüğünüzde hello Microsoft omurga ulaştınız bilirsiniz.<br><br>
![Gecikme olmadığı denetleniyor](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi veya Yardım için bağlantılar aşağıdaki hello denetleyin:

- [Azure sanal makineleri için ağ verimliliğini en iyi duruma getirme](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Microsoft Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
