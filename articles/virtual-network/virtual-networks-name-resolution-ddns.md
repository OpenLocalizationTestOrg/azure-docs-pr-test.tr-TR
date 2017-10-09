---
title: "aaaUsing dinamik DNS tooregister ana bilgisayar adları"
description: "Bu sayfa hakkında ayrıntılar verir tooset kendi DNS sunucularınızı dinamik DNS tooregister konak adları ayarlama."
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a>Dinamik DNS tooregister ana bilgisayar adları kendi DNS sunucusu kullanma
[Azure ad çözümlemesi sağlar](virtual-networks-name-resolution-for-vms-and-role-instances.md) sanal makineleri (VM'ler) ve rol örnekleri için. Ancak, ad çözümlemesi Azure tarafından sağlanan ötesinde olduğunuzda, kendi DNS sunucularınızı sağlayabilir. DNS çözüm toosuit güç tootailor hello kazandırır belirli gereksinimlerinizi. Örneğin, Active Directory etki alanı denetleyicinizi tooaccess şirket içi kaynakları gerekebilir.

Azure VM'ler, iletebileceği özel DNS sunucularınızın barındırıldığında hostname Merhaba aynı sorgular vnet tooAzure tooresolve ana bilgisayar adları. Bu yol toouse istemiyorsanız, VM ana bilgisayar adları DNS sunucunuzun dinamik DNS kullanarak kaydedebilirsiniz.  Azure alternatif düzenlemeleri genellikle gerektiği şekilde kayıtları, DNS sunucularınızın oluşturmak hello özelliği (örneğin, kimlik bilgileri) toodirectly sahip değil. Burada, Alternatiflerle birlikte ortak bazı senaryolar vardır.

## <a name="windows-clients"></a>Windows istemcileri
Olmayan etki alanına katılmış Windows istemcileri güvenli olmayan dinamik DNS (DDNS) güncelleştirmeleri bunlar önyüklediğinizde veya IP adreslerini değiştiğinde çalışır. Merhaba DNS hello hostname artı hello birincil DNS soneki adıdır. Azure hello birincil DNS soneki boş bırakır, ancak hello VM hello aracılığıyla bu ayarlayabilirsiniz [UI](https://technet.microsoft.com/library/cc794784.aspx) veya [Otomasyon kullanarak](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).

Etki alanına katılmış Windows istemcileri güvenli dinamik DNS kullanarak IP adreslerini hello etki alanı denetleyicisi ile kaydedin. Merhaba etki alanına katılma işlemi hello istemcide hello birincil DNS soneki ayarlar ve oluşturur ve hello güven ilişkisini korur.

## <a name="linux-clients"></a>Linux istemcileri
Linux istemcileri genellikle başlangıçta hello DNS sunucusuyla kendilerini yok, hello DHCP sunucusu mevcut varsayalım. Azure'nın DHCP sunucuları, DNS sunucusu veya kimlik bilgilerini tooregister kayıtları hello yeteneği yok.  Adlı bir aracı kullanabilirsiniz *nsupdate*hello bağlama paketine dahil, dinamik DNS toosend güncelleştirir. Merhaba dinamik DNS protokolü standartlaştırılmış için kullanabileceğiniz *nsupdate* bile zaman bağlama hello DNS sunucusunda kullanmakta olduğunuz değil.

Merhaba hostname hello DNS sunucusu girişi korumak ve hello DHCP istemci toocreate tarafından sağlanan hello kancaları kullanın. Merhaba DHCP döngüsü sırasında hello istemci hello komut dosyalarında yürütür */etc/dhcp/dhclient-exit-hooks.d/*. Bu, tooregister hello yeni IP adresini kullanarak kullanılan *nsupdate*. Örneğin:

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

Merhaba de kullanabilirsiniz *nsupdate* komutu tooperform güvenli dinamik DNS güncelleştirir. Örneğin, bir BIND DNS sunucusu kullanırken, bir genel-özel anahtar çifti [oluşturulan](http://linux.yyz.us/nsupdate/).  Merhaba DNS sunucusu [yapılandırılmış](http://linux.yyz.us/dns/ddns-server.html) hello ortak anahtarının bir parçası olan hello isteği hello imza doğrulayabilmeniz için hello ile. Merhaba kullanmalısınız *-k* seçeneği tooprovide hello anahtar çifti çok*nsupdate* hello için dinamik DNS güncelleştirme imzalı istek toobe sırayla.

Bir Windows DNS sunucusu kullanırken, Kerberos kimlik doğrulaması ile Merhaba kullanabilirsiniz *-g* parametresinde *nsupdate* (Merhaba Windows sürümünde kullanılabilir *nsupdate* ). toodo Bu, kullanım *kinit* tooload hello kimlik bilgilerini (örneğin bir [keytab dosya](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)). Ardından *nsupdate -g* hello önbelleğinden hello kimlik bilgileri çeker.

Gerekli olursa, DNS Arama soneki tooyour VM'ler ekleyebilirsiniz. Merhaba DNS soneki hello belirtilen */etc/resolv.conf* dosya. Çoğu Linux distro'lar hello içeriği otomatik olarak yönetir bu dosya, bu nedenle genellikle düzenleyemezsiniz. Ancak, hello DHCP istemcisinin kullanarak hello soneki geçersiz kılabilirsiniz *yerine geçen* komutu. toodo Bu, */etc/dhcp/dhclient.conf*, ekleyin:

        supersede domain-name <required-dns-suffix>;

