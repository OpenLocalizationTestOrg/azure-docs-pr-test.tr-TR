---
title: "IPv6 - Azure şablonu ile bir Internet'e yönelik Yük Dengeleyici aaaDeploy | Microsoft Docs"
description: "Nasıl toodeploy IPv6 Azure yük dengeleyici ve Yük Dengelemesi VM'ler için destek."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
keywords: "IPv6, azure yük dengeleyici, çift yığın, genel IP, yerel IPv6, mobil, IOT"
ms.assetid: 2998e943-13fc-4ea9-a68c-875e53a08db3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2016
ms.author: kumud
ms.openlocfilehash: 68b9ba874a50161243577b64c4a6d9c76b39156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-internet-facing-load-balancer-solution-with-ipv6-using-a-template"></a>Bir şablonu kullanarak bir Internet'e yönelik Yük Dengeleyici çözümü IPv6 ile dağıtma

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Azure CLI](load-balancer-ipv6-internet-cli.md)
> * [Şablon](load-balancer-ipv6-internet-template.md)

Azure Load Balancer bir Katman 4 (TCP, UDP) yük dengeleyicidir. Merhaba yük dengeleyici, gelen trafiği bulut Hizmetleri sağlıklı hizmet örnekleri veya bir yük dengeleyici kümesindeki sanal makineler arasında dağıtarak yüksek kullanılabilirlik sağlar. Ayrıca, Azure Load Balancer bu hizmetleri birden çok bağlantı noktasında, birden çok IP adresinde ya da her ikisinde birden sağlayabilir.

## <a name="example-deployment-scenario"></a>Örnek dağıtım senaryosu

Merhaba Aşağıdaki diyagramda gösterilmektedir hello yük dengeleme çözümü bu makalede açıklanan hello örnek şablon kullanılarak dağıtılan.

![Yük dengeleyici senaryosu](./media/load-balancer-ipv6-internet-template/lb-ipv6-scenario.png)

Bu senaryoda aşağıdaki Azure kaynakları hello oluşturacak:

* atanan IPv4 ve IPv6 adreslerinin her VM için bir sanal ağ arabirimi
* bir IPv4 ve IPv6 genel IP adresi olan bir Internet'e yönelik Yük Dengeleyici
* iki Yük Dengeleme kuralları toomap hello ortak VIP'ler toohello özel uç noktaları
* Merhaba iki VM'ler içeren bir kullanılabilirlik kümesi
* iki sanal makine (VM)

## <a name="deploying-hello-template-using-hello-azure-portal"></a>Hello Azure portal kullanarak hello şablonu dağıtma

Bu makalede hello yayımlanan bir şablon başvuran [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/201-load-balancer-ipv6-create/) Galerisi. Merhaba Galerisi'nden hello şablonunu indirebilir ya da doğrudan hello galerisinden azure'da hello dağıtım Başlat. Bu makalede hello şablonu tooyour yerel bilgisayara yüklediğiniz varsayılır.

1. Hello Azure portal ve izinleri toocreate VM'ler ve bir Azure aboneliği içindeki ağ kaynaklara sahip bir hesapla oturum açın. Ayrıca, var olan kaynakların kullanmadığınız sürece hello hesabının izni toocreate bir kaynak grubu ve bir depolama hesabı gerekir.
2. Tıklayın "+ Yeni" Merhaba menü silip hello arama kutusuna "Şablon" türü. "Şablon dağıtımı" Merhaba Arama sonuçlarından seçin.

    ![IPv6 portal Adım2 lb](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step2.png)

3. İçindeki her şeyi hello dikey penceresinde "Şablon dağıtımı"'i tıklatın

    ![lb-IPv6-portal-adım 3](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step3.png)

4. "Oluştur" seçeneğini tıklatın

    ![IPv6 portal step4 lb](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step4.png)

5. "Şablonu Düzenle" seçeneğini tıklatın. Merhaba varolan içeriğini silin ve kopyala/yapıştır hello tüm hello şablon dosyasının içeriği (tooinclude hello başlangıç ve bitiş {}), "Kaydet"'i tıklatın

    > [!NOTE]
    > Microsoft Internet Explorer kullanıyorsanız, Yapıştır açtığınızda tooallow erişim toohello Windows panosuna soran bir iletişim kutusu görüntülenir. "Erişime izin ver."'i tıklatın

    ![IPv6 portal step5 lb](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step5.png)

6. "Parametreleri Düzenle" seçeneğini tıklatın. Hello parametreler dikey penceresinde hello şablon parametreleri bölümüne hello rehberliğinde hello değerleri belirtin, sonra tooclose hello parametreler dikey "Kaydet"'i tıklatın. Merhaba özel dağıtım dikey penceresinde, aboneliğiniz, varolan bir kaynak grubu seçin veya oluşturun. Bir kaynak grubu oluşturuyorsanız, hello kaynak grubu için bir konum seçin. Bundan sonra öğesini **yasal koşulları**, ardından **satın alma** hello yasal koşulları için. Azure hello kaynakları dağıtmaya başlar. İşlem birkaç dakika toodeploy tüm hello kaynakları alır.

    ![IPv6 portal step6 lb](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step6.png)

    Hello Bu parametreler hakkında daha fazla bilgi için bkz: [şablon parametreleri ve değişkenleri](#template-parameters-and-variables) bu makalenin sonraki bölümlerinde bölümü.

7. Merhaba şablonu tarafından oluşturulan toosee hello kaynakları Gözat'ı tıklatın, "Kaynak grupları" konusuna bakın ve ardından tıklatın kadar hello listede aşağı kaydırın.

    ![IPv6 portal step7 lb](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step7.png)

8. Hello kaynak grupları dikey penceresinde hello 6. adımda belirttiğiniz hello kaynak grubunun adını tıklatın. Dağıtılan tüm hello kaynakların bir listesini görürsünüz. Tüm iyi olursa, "Başarılı" özelliğini "Son dağıtım altında" yazması gerekir Aksi durumda, kullanmakta olduğunuz hello hesap izinleri toocreate hello gerekli kaynaklara sahip olduğundan emin olun.

    ![IPv6 portal step8 lb](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step8.png)

    > [!NOTE]
    > 6. adım tamamlandıktan hemen sonra kaynak grupları göz atarsanız, "Son dağıtım" Merhaba kaynakları dağıtılırken "Dağıtma" Merhaba durumunu görüntüler.

9. Kaynakların hello listesinde "myIPv6PublicIP"'i tıklatın. Bir IPv6 adresi IP adresi altında olduğunu ve DNS adını adım 6 hello dnsNameforIPv6LbIP parametresi için belirtilen hello değeri olduğunu görürsünüz. Bu kaynak erişilebilir tooInternet istemcileri olan hello genel IPv6 adresi ve ana bilgisayar adıdır.

    ![IPv6 portal step9 lb](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step9.png)

## <a name="validate-connectivity"></a>Bağlantı doğrula

Merhaba şablonu başarıyla dağıtıldığını, görevleri aşağıdaki hello tamamlayarak bağlantı doğrulayabilirsiniz:

1. Toohello Azure portalında oturum ve hello hello şablon dağıtımı tarafından oluşturulan VM'ler tooeach bağlanın. İpconfig komutunu çalıştırmak bir Windows Server VM dağıttıysanız/bir komut isteminden tüm. Hello VM'ler IPv4 ve IPv6 adresleri olduğunu görürsünüz. Linux VM'ler dağıttıysanız, Linux dağıtımınız için sağlanan hello yönergeleri kullanarak tooconfigure hello Linux işletim sistemi tooreceive dinamik IPv6 adresleri gerekir.
2. IPv6 Internet'e bağlı bir istemciden bir bağlantı toohello genel IPv6 adresi hello yük dengeleyici başlatır. Yük Dengeleyici hello tooconfirm hello iki VM'ler arasında Dengeleme, bir web sunucusu Microsoft Internet Information Services (IIS) gibi hello VM'lerin her birinde yükleyebilir. Merhaba varsayılan web sayfası her sunucuda "Server0" Merhaba metin içerebilir veya "SUNUCU1" toouniquely belirleyin. Ardından, bir IPv6 Internet'e bağlı istemci bir Internet tarayıcısında açın ve hello dnsNameforIPv6LbIP parametresi hello yük dengeleyici tooconfirm uçtan uca IPv6 bağlantısı tooeach VM için belirtilen toohello ana bilgisayar adını bulun. Yalnızca tek bir sunucudan hello web sayfasını görürseniz, tarayıcı önbelleğiniz tooclear gerekebilir. Birden çok özel tarayıcı oturumu açın. Her sunucusundan bir yanıt görmeniz gerekir.
3. IPv4 Internet'e bağlı bir istemciden bağlantı toohello genel bir IPv4 adresi hello yük dengeleyicinin başlatır. Yük Dengeleyici hello tooconfirm olan iki VM Yük Dengeleme Merhaba, 2. adım ayrıntılı olarak IIS, kullanarak test edebilirsiniz.
4. Her sanal makineden bir giden bağlantı tooan IPv6 ya da IPv4 bağlı Internet aygıtı başlatır. Her iki durumda da hello hedef aygıt tarafından görülen hello kaynak IP hello ortak IPv4 veya IPv6 hello yük dengeleyici adresidir.

> [!NOTE]
> IPv4 ve IPv6 için ICMP hello Azure ağ engellendi. Sonuç olarak, her zaman ping gibi ICMP Araçlar başarısız. tootest bağlantısı, bir TCP alternatif TCPing gibi kullanın veya PowerShell Test-NetConnection cmdlet'i hello. Başlangıç IP adresi Hello diyagramda gösterildiği örnek görebileceğiniz değerler olduğunu unutmayın. Dinamik olarak atanmış Hello IPv6 adresleri olduğundan, aldığınız hello adresleri farklılık gösterir ve bölgeye göre farklılık gösterebilir. Ayrıca, özel IPv6 adresleri hello arka uç havuzundaki hello daha farklı bir önek ile Merhaba yük dengeleyici toostart hello genel IPv6 adresi için yaygındır.

## <a name="template-parameters-and-variables"></a>Şablon parametreleri ve değişkenleri

Bir Azure Resource Manager şablonu birden fazla değişkenleri ve parametreleri tooyour gereksinimlerini özelleştirebilirsiniz içerir. Değişkenleri, bir kullanıcı toochange istiyor musunuz sabit değerler için kullanılır. Parametreler için değerler hello şablonu dağıtırken kullanıcı tooprovide istediğiniz kullanılır. Merhaba örnek şablonu, bu makalede açıklanan hello senaryosu için yapılandırıldı. Bu tooneeds ortamınızın özelleştirebilirsiniz.

Bu makalede kullanılan şablon içerir hello aşağıdaki hello örnek değişkenleri ve parametreleri:

| Parametre / değişken | Notlar |
| --- | --- |
| adminUsername |Merhaba hello yönetici hesabının adını toosign toohello sanal makinelerle kullanılan belirtin. |
| Admınpassword |Merhaba yönetici hesabının parolasını Hello toosign toohello sanal makinelerle kullanılan belirtin. |
| dnsNameforIPv4LbIP |Merhaba ortak adı hello yük dengeleyici olarak tooassign istediğiniz hello DNS ana bilgisayar adı belirtin. Bu ad toohello yük dengeleyicinin genel IPv4 adresine çözümler. Merhaba adı küçük harfli olması ve eşleşen hello regex: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. |
| dnsNameforIPv6LbIP |Merhaba ortak adı hello yük dengeleyici olarak tooassign istediğiniz hello DNS ana bilgisayar adı belirtin. Bu ad toohello yük dengeleyicinin genel IPv6 adresi çözümler. Merhaba adı küçük harfli olması ve eşleşen hello regex: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. Bu hello olabilir IPv4 adresi hello gibi aynı adı. Bir istemci gönderdiğinde hello adı paylaşıldığında bu Azure ad için bir DNS sorgusu hello A ve AAAA kayıt döndürür. |
| vmNamePrefix |Merhaba VM adı öneki belirtin. Merhaba şablon ekler bir sayı (0, 1, vb.) toohello adı hello zaman VM'ler oluşturulur. |
| nicNamePrefix |Merhaba ağ arabirimi adı ön ekini belirtin. Merhaba şablon ekler bir sayı (0, 1, vb.) hello ağ arabirimleri oluşturulduğunda toohello adı. |
| storageAccountName |Mevcut bir depolama hesabını Hello adını girin veya hello şablonu tarafından oluşturulan yeni bir tek toobe hello adını belirtin. |
| availabilitySetName |Merhaba VM'ler ile kullanılan toobe hello kullanılabilirlik adını ayarlayın, sonra da girin |
| addressPrefix |Merhaba adres öneki toodefine hello hello sanal ağ adres aralığı kullanılan |
| subnetName |Merhaba VNet hello alt ağda Hello adını oluşturuldu |
| subnetPrefix |Merhaba adres öneki toodefine hello hello alt ağ adres aralığı kullanılan |
| vnetName |Merhaba hello VM'ler tarafından kullanılan VNet Hello adını belirtin. |
| ipv4PrivateIPAddressType |Merhaba ayırma yöntemi için hello özel IP adresi (statik veya dinamik) kullanılır. |
| ipv6PrivateIPAddressType |Merhaba ayırma yöntemi için hello özel IP adresi (dinamik) kullanılır. IPv6, yalnızca dinamik ayırma destekler. |
| numberOfInstances |örnekleri hello şablon tarafından dağıtılan Hello sayısı yük dengeli |
| ipv4PublicIPAddressName |Merhaba ortak IPv4 adresiyle hello yük dengeleyicinin toouse toocommunicate istediğiniz hello DNS adını belirtin. |
| ipv4PublicIPAddressType |Hello için genel IP adresi (statik veya dinamik) kullanılan hello ayırma yöntemi |
| Ipv6PublicIPAddressName |Merhaba genel IPv6 adresi hello yük dengeleyici ile toouse toocommunicate istediğiniz hello DNS adını belirtin. |
| ipv6PublicIPAddressType |Hello için genel IP adresi (dinamik) kullanılan hello ayırma yöntemi. IPv6, yalnızca dinamik ayırma destekler. |
| lbName |Merhaba yük dengeleyici Hello adını belirtin. Bu ad hello Portalı'nda görüntülenen veya CLI veya PowerShell komutuyla tooit söz konusu olduğunda kullanılır. |

Merhaba şablondaki kalan değişkenleri Hello Azure hello kaynakları oluşturduğunda, atanmış olan türetilmiş değerlerini içerir. Bu değişkenleri değiştirmeyin.
