---
title: "İlk Azure sanal ağ aaaCreate | Microsoft Docs"
description: "Nasıl toocreate bir Azure sanal ağı (VNet), iki sanal makine (VM) toohello VNet bağlanmak ve toohello VM'ler bağlanmak öğrenin."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2016
ms.author: jdial
ms.openlocfilehash: 1981524cf706d5ebc83b1ff77735617550ff058a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-virtual-network"></a>İlk sanal ağınızı oluşturma

Toocreate iki alt ağ ile sanal ağ (VNet) iki sanal makine (VM) oluşturma ve hello ağların her VM tooone bağlanmak hello resim aşağıdaki gösterildiği gibi öğrenin:

![Sanal ağ diyagramı](./media/virtual-network-get-started-vnet-subnet/vnet-diagram.png)

Bir Azure sanal ağı (VNet), kendi ağ hello bulutta gösterimidir. Azure ağ ayarlarınızı kontrol edebilir ve DHCP adres bloklarını, DNS ayarlarını, güvenlik ilkelerini ve yönlendirmeyi tanımlayabilirsiniz. Merhaba okuma VNet kavramları hakkında daha fazla toolearn [Virtual Network'e genel bakış](virtual-networks-overview.md) makalesi. Aşağıdaki adımları toocreate hello kaynakları Hello resimde gösterilen hello tamamlayın:

1. [İki alt ağı olan bir sanal ağ oluşturma](#create-vnet)
2. [Her bir ağ arabirimine (NIC) sahip iki VM oluşturma](#create-vms)ve bir ağ güvenlik grubu (NSG) tooeach NIC ilişkilendirin
3. [Sanal makineleri hello tooand Bağlan](#connect-to-from-vms)
4. [Tüm kaynakları silme](#delete-resources). Sağlanan durumdayken bu alıştırmada oluşturulan hello kaynaklardan bazıları için ücretler uygulanır. toominimize hello ücretleri hello alıştırma tamamladıktan sonra oluşturduğunuz bu bölümde toodelete hello kaynaklarında toocomplete hello adımları emin olun.

Tamamlanıyor hello bu makaledeki adımları sonra VNet nasıl kullanabileceğiniz, temel bilgilere sahip. Sonraki adımlar hakkında daha fazla bilgi için sağlanan toouse daha ayrıntılı bir düzeyde sanal ağlar.

## <a name="create-vnet"></a>İki alt ağa sahip bir sanal ağ oluşturma

toocreate izleyin tam hello adımları iki alt ağa sahip bir sanal ağ. Farklı alt ağlardır genellikle toocontrol hello alt ağlar arasındaki trafik akışını kullanılır.

1. İçinde toohello oturum [Azure portal](<https://portal.azure.com>). Henüz bir hesabınız yoksa, [bir aylık ücretsiz denemeye](https://azure.microsoft.com/free) kaydolabilirsiniz. 
2. Merhaba, **Sık Kullanılanlar** hello portalının bölmesi **yeni**.
3. Merhaba, **yeni** dikey penceresinde tıklatın **ağ**. Merhaba, **ağ** dikey penceresinde tıklatın **sanal ağ**hello resim aşağıdaki gösterildiği gibi:

    ![Sanal ağ diyagramı](./media/virtual-network-get-started-vnet-subnet/virtual-network.png)

4.  Merhaba, **sanal ağ** dikey penceresinde, bırakın *Resource Manager* hello dağıtım modeli ve tıklatın seçilen **oluşturma**.
5.  Merhaba, **oluşturma sanal ağ dikey** görüntülenir, değerleri aşağıdaki hello girin, ardından tıklatın **oluşturma**:

    |**Ayar**|**Değer**|**Ayrıntılar**|
    |---|---|---|
    |**Ad**|*MyVNet*|Merhaba adı hello kaynak grubun içinde benzersiz olmalıdır.|
    |**Adres alanı**|*10.0.0.0/16*|CIDR gösteriminde istediğiniz herhangi bir adres alanını belirtebilirsiniz.|
    |**Alt ağ adı**|*Ön uç*|Merhaba alt ağ adı hello sanal ağ içinde benzersiz olmalıdır.|
    |**Alt ağ adres aralığı**|*10.0.0.0/24*| Belirttiğiniz hello aralığındaki hello sanal ağ için tanımlı hello adres alanı içinde bulunmalıdır.|
    |**Abonelik**|*[Aboneliğiniz]*|Bir abonelik toocreate hello VNet seçin içinde. Bir sanal ağ, tek bir abonelik içinde bulunabilir.|
    |**Kaynak grubu**|**Yeni oluştur:** *MyRG*|Bir kaynak grubu oluşturun. Merhaba kaynak grubu adı, seçtiğiniz hello abonelik içinde benzersiz olmalıdır. Merhaba okuyun, kaynak grupları hakkında daha fazla toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) genel bakış makalesi.|
    |**Konum**|*Batı ABD*| Genellikle en yakın tooyour fiziksel konumu hello konumu seçilir.|

    VNet alır, birkaç saniye toocreate hello. Oluşturulduktan sonra gördüğünüz hello Azure portalı panosunun.

6. Oluşturulan, hello Azure portal hello sanal ağ ile **Sık Kullanılanlar** bölmesinde tıklatın **tüm kaynakları**. Merhaba tıklatın **MyVNet** hello sanal ağında **tüm kaynakları** dikey. Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz *MyVNet* hello içinde **ada göre Filtrele...** kutusunu tooeasily erişim hello VNet.
7. Merhaba **MyVNet** dikey penceresi açılır ve hello resim aşağıdaki gösterildiği gibi hello Vnet'in hakkındaki bilgileri görüntüler:

    ![Sanal ağ diyagramı](./media/virtual-network-get-started-vnet-subnet/myvnet.png)

8. Merhaba önceki resimde gösterildiği gibi tıklayın **alt ağlar** toodisplay hello VNet içinde hello alt ağların bir listesi. Merhaba bulunan alt ağıdır **ön uç**, 5. adımda oluşturduğunuz alt hello.
9. Merhaba MyVNet - alt ağlar dikey penceresini tıklatın **+ alt** toocreate hello sahip bir alt ağa bilgileri ve tıklatın ardından **Tamam** toocreate hello alt ağ:

    |**Ayar**|**Değer**|**Ayrıntılar**|
    |---|---|---|
    |**Ad**|*Arka uç*|Merhaba adı hello sanal ağ içinde benzersiz olmalıdır.|
    |**Adres aralığı**|*10.0.1.0/24*|Belirttiğiniz hello aralığındaki hello sanal ağ için tanımlı hello adres alanı içinde bulunmalıdır.|
    |**Ağ güvenlik grubu** ve **Yol tablosu**|*Hiçbiri* (varsayılan)|Ağ güvenlik grupları (NSG’ler) b makalenin sonraki bölümlerinde ele alınmıştır. Merhaba okuyun, kullanıcı tanımlı yollar hakkında daha fazla toolearn [kullanıcı tanımlı yollar](virtual-networks-udr-overview.md) makalesi.|

10. Yeni bir alt ağ Hello toohello VNet eklendikten sonra hello kapatabilirsiniz **MyVNet – alt ağlar** dikey sonra Kapat hello **tüm kaynakları** dikey.

## <a name="create-vms"></a>Sanal makineler oluşturma

Merhaba VNet ve alt ağları oluşturulan ile Merhaba VM'ler oluşturabilirsiniz. Bu alıştırmada, hello Windows Server işletim sistemi çalıştıran her iki VM yine de birkaç farklı Linux dağıtımları dahil olmak üzere Azure tarafından desteklenen herhangi bir işletim sistemini çalıştırabilirler.

### <a name="create-web-server-vm"></a>Merhaba web sunucusu VM oluşturma

toocreate hello web sunucusu VM, aşağıdaki adımları tam hello:

1. Hello Azure portal Sık Kullanılanlar bölmesinde **yeni**, **işlem**, ardından **Windows Server 2016 Datacenter**.
2. Merhaba, **Windows Server 2016 Datacenter** dikey penceresinde tıklatın **oluşturma**.
3. Merhaba, **Temelleri** görünür, dikey girin veya seçin değerleri aşağıdaki hello ve tıklatın **Tamam**:

    |**Ayar**| **Değer**|**Ayrıntılar**|
    |---|---|---|
    |**Ad**|*MyWebServer*|Bu VM, İnternet kaynaklarının bağlı olduğu bir web sunucusu işlevi görür.|
    |**VM disk türü**|*SSD*|
    |**Kullanıcı adı**|*Tercih ettiğiniz*|
    |**Parola ve Parolayı onayla**|*Tercih ettiğiniz*|
    | **Abonelik**|*<Your subscription>*|Merhaba abonelik olmalıdır hello hello 5 adımda seçtiğiniz aynı abonelik [iki alt ağa sahip bir sanal ağ oluşturma](#create-vnet) bu makalenin. Merhaba VM toomust bağlandığınız VNet mevcut hello aynı VM hello gibi abonelik.|
    |**Kaynak grubu**|**Var olanı kullan:** *MyRG* öğesini seçin|Aynı kaynak grubunu Merhaba Vnet'in yaptığımız gibi hello hello kullanmakta olduğunuz olsa kaynakları hello tooexist yok aynı kaynak grubu.|
    |**Konum**|*Batı ABD*|Başlangıç konumu olmalıdır hello hello 5. adımında belirtilen aynı konuma [iki alt ağa sahip bir sanal ağ oluşturma](#create-vnet) bu makalenin. VM'ler ve sanal ağlar toomust bağlandıklarında hello mevcut hello aynı konumu.|

4. Merhaba, **bir boyutu seçin** dikey penceresinde tıklatın *DS1_V2 standart*, ardından **seçin**. Okuma hello [Windows VM boyutları](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesine bir listesi için Azure tarafından desteklenen tüm Windows VM boyutları.
5. Merhaba, **ayarları** dikey penceresinde girin veya seçin değerleri aşağıdaki hello ve tıklatın **Tamam**:

    |**Ayar**|**Değer**|**Ayrıntılar**|
    |---|---|---|
    |**Depolama: Yönetilen diskler kullan**|*Evet*||
    |**Sanal ağ**| *MyVNet* öğesini seçin|Hello aynı mevcut VNet seçebileceğiniz oluşturduğunuz VM hello gibi konumu. sanal ağlar ve alt ağları, hello okuma hakkında daha fazla toolearn [sanal ağ](virtual-networks-overview.md) makalesi.|
    |**Alt ağ**|*Ön uç*’u seçin|Merhaba VNet içinde mevcut herhangi bir alt ağ seçebilirsiniz.|
    |**Genel IP adresi**|Merhaba varsayılanı kabul edin|Bir ortak IP adresi, tooconnect toohello VM hello Internet gelen sağlar. Merhaba okuma genel IP adresleri hakkında daha fazla toolearn [IP adreslerini](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) makalesi.|
    |**Ağ güvenlik grubu (güvenlik duvarı)**|Merhaba varsayılanı kabul edin|Merhaba tıklatın **(yeni) MyWebServer nsg** varsayılan NSG hello portal ayarlarını tooview oluşturuldu. Merhaba, **oluşturma ağ güvenlik grubu** açar dikey penceresinde, bir gelen herhangi bir kaynak IP adresine gelen TCP/3389 (RDP) trafiğine izin verir kuralı sahip dikkat edin.|
    |**Diğer tüm değerler**|Merhaba Varsayılanları kabul edin|toolearn hello okuma ayarları, kalan hello hakkında daha fazla [hakkında VM'ler](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi.|

    Ağ güvenlik grupları (NSG), hello hello VM gelen tooand akabilir ağ trafiği türü için toocreate gelen/giden kuralları etkinleştirin. Varsayılan olarak, tüm gelen trafiği toohello VM reddedildi. Bir üretim web sunucusu için, TCP/80 (HTTP) ve TCP/443 (HTTPS) için ilave gelen kuralları ekleyebilirsiniz. Varsayılan olarak, giden trafik için kural yoktur, tüm giden trafiğe izin verilir. Ekleme/kuralları toocontrol trafiği ilkelerinizi kaldırabilirsiniz. Okuma hello [ağ güvenlik grupları](virtual-networks-nsg.md) makale toolearn Nsg'ler hakkında daha fazla bilgi.

6.  Merhaba, **Özet** dikey penceresinde hello ayarlarını gözden geçirin ve tıklatın **Tamam** toocreate hello VM. Durumu kutucuğu hello portal panosunda VM oluşturur hello görüntülenir. Birkaç dakika toocreate sürebilir. Toocomplete için toowait gerekmez. VM oluşturulan hello sırasında toohello sonraki adıma devam edebilirsiniz.

### <a name="create-database-server-vm"></a>Merhaba veritabanı sunucusu VM oluşturma

toocreate hello veritabanı sunucusu VM, aşağıdaki adımları tam hello:

1.  Merhaba Sık Kullanılanlar bölmesinde **yeni**, **işlem**, ardından **Windows Server 2016 Datacenter**.
2.  Merhaba, **Windows Server 2016 Datacenter** dikey penceresinde tıklatın **oluşturma**.
3.  Merhaba, **temel bilgiler dikey penceresindeki**girin veya değerleri aşağıdaki hello seçin ve ardından tıklatın **Tamam**:

    |**Ayar**|**Değer**|**Ayrıntılar**|
    |---|---|---|
    |**Ad**|*MyDBServer*|Bu VM hello web sunucusuna bağlanır, ancak Internet bağlanılamıyor bu hello bir veritabanı sunucusu olarak görev yapar.|
    |**VM disk türü**|*SSD*||
    |**Kullanıcı adı**|Tercih ettiğiniz||
    |**Parola ve Parolayı onayla**|Tercih ettiğiniz||
    |**Abonelik**|<Your subscription>|Merhaba abonelik olmalıdır hello hello adım 5'te seçtiğiniz aynı abonelik [iki alt ağa sahip bir sanal ağ oluşturma](#create-vnet) bu makalenin.|
    |**Kaynak grubu**|**Var olanı kullan:** *MyRG* öğesini seçin|Aynı kaynak grubunu Merhaba Vnet'in yaptığımız gibi hello hello kullanmakta olduğunuz olsa kaynakları hello tooexist yok aynı kaynak grubu.|
    |**Konum**|*Batı ABD*|Başlangıç konumu olmalıdır hello hello 5. adımında belirtilen aynı konuma [iki alt ağa sahip bir sanal ağ oluşturma](#create-vnet) bu makalenin.|

4.  Merhaba, **bir boyutu seçin** dikey penceresinde tıklatın *DS1_V2 standart*, ardından **seçin**.
5.  Merhaba, **ayarları** dikey penceresinde girin veya seçin değerleri aşağıdaki hello ve tıklatın **Tamam**:

    |**Ayar**|**Değer**|**Ayrıntılar**|
    |----|----|---|
    |**Depolama: Yönetilen diskler kullan**|*Evet*||
    |**Sanal ağ**|*MyVNet* öğesini seçin|Hello aynı mevcut VNet seçebileceğiniz oluşturduğunuz VM hello gibi konumu.|
    |**Alt ağ**|Seçin *arka uç* hello tıklayarak **alt** kutusu seçilerek, **arka uç** hello gelen **bir alt ağ seçin** dikey penceresi|Merhaba VNet içinde mevcut herhangi bir alt ağ seçebilirsiniz.|
    |**Genel IP adresi**|Hiçbiri – hello varsayılan adres'ı tıklatın **hiçbiri** hello gelen **genel IP adresi seçin** dikey penceresi|Bir ortak IP adresi olmadan, yalnızca başka bir VM bağlı toohello toohello VM bağlanabilir aynı sanal ağı. Merhaba doğrudan Internet tooit bağlanamıyor.|
    |**Ağ güvenlik grubu (güvenlik duvarı)**|Merhaba varsayılanı kabul edin| NSG Merhaba MyWebServer VM bu NSG da oluşturmuş hello varsayılan hello sahip gibi aynı gelen varsayılan kural. Bir veritabanı sunucusu için TCP/1433 (MS SQL) için ek bir gelen kuralı ekleyebilirsiniz. Varsayılan olarak, giden trafik için kural yoktur, tüm giden trafiğe izin verilir. Ekleme/kuralları toocontrol trafiği ilkelerinizi kaldırabilirsiniz.|
    |**Diğer tüm değerler**|Merhaba Varsayılanları kabul edin||

6.  Merhaba, **Özet** dikey penceresinde hello ayarlarını gözden geçirin ve tıklatın **Tamam** toocreate hello VM. Durumu kutucuğu hello portal panosunda VM oluşturur hello görüntülenir. Birkaç dakika toocreate sürebilir. Toocomplete için toowait gerekmez. VM oluşturulan hello sırasında toohello sonraki adıma devam edebilirsiniz.

## <a name="review"></a>Kaynakları gözden geçirme

Ancak bir sanal ağ ve iki VM, hello birkaç ek kaynaklar için hello MyRG kaynak grubunda oluşturduğunuz Azure portalında oluşturduğunuz. Merhaba MyRG kaynak grubu Merhaba içeriğine hello aşağıdaki adımları tamamlayarak gözden geçirin:

1. Merhaba, **Sık Kullanılanlar** bölmesinde tıklatın **daha fazla hizmet**.
2. Merhaba, **daha fazla hizmet** bölmesi, türü *kaynak grupları* hello word hello kutusundaki *filtre* da. Tıklatın **kaynak grupları** hello gördüğünüzde filtre listesi.
3. Merhaba, **kaynak grupları** bölmesinde hello tıklatın *MyRG* kaynak grubu. Aboneliğinizde var olan birçok kaynak grupları varsa, yazabilirsiniz *MyRG* hello metni içeren hello kutusunda *ada göre Filtrele...* tooquickly erişim hello MyRG kaynak grubu.
4.  Merhaba, **MyRG** dikey penceresinde, gördüğünüz hello kaynak grubunun 12 kaynaklar içeriyor hello resim aşağıdaki gösterildiği gibi:

    ![Kaynak grubu içeriği](./media/virtual-network-get-started-vnet-subnet/resource-group-contents.png)

VM'ler, diskler ve depolama hesapları, hello okuma hakkında daha fazla toolearn [sanal makine](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [Disk](../virtual-machines/windows/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-network%2ftoc.json), ve [depolama hesabı](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) genel bakış makaleleri. Merhaba iki varsayılan Nsg'ler hello portal sizin için oluşturduğu görebilirsiniz. Oluşturulan iki ağ arabirimi (NIC) kaynakları hello portalınız de görebilirsiniz. Bir NIC hello VNet üzerinde bir VM tooconnect tooother kaynakları sağlar. Okuma hello [NIC](virtual-network-network-interface.md) makale toolearn NIC'ler hakkında daha fazla bilgi. Merhaba portalı da bir genel IP adresi kaynak oluşturmuştur. Genel IP adresleri, genel bir IP adresi kaynağı için bir ayardır. Merhaba okuma genel IP adresleri hakkında daha fazla toolearn [IP adreslerini](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) makalesi.

## <a name="connect-to-from-vms"></a>Toohello VM'ler Bağlan

Sanal ağınızı ve oluşturulan iki VM, aşağıdaki bölümlerde hello hello adımları tamamlayarak toohello VM'ler şimdi bağlanabilir:

### <a name="connect-from-internet"></a>Internet hello toohello web sunucusu VM Bağlan

tooconnect toohello web sunucusundan VM hello Internet, aşağıdaki adımları tam hello:

1. Merhaba Portalı'nda Aç hello MyRG kaynak grubu'hello tamamlayarak hello adımları [gözden kaynakları](#review) bu makalenin.
2. Merhaba, **MyRG** dikey penceresinde hello tıklatın **MyWebServer** VM.
3. Merhaba, **MyWebServer** dikey penceresinde tıklatın **Bağlan**hello resim aşağıdaki gösterildiği gibi:

    ![Tooweb sunucuya VM](./media/virtual-network-get-started-vnet-subnet/webserver.png)

4. Tarayıcı toodownload hello izin *MyWebServer.rdp* dosya ve ardından açın.
5. Bu hello yayımcısına hello uzak bağlantı doğrulanamıyor bildiren bir iletişim kutusu alırsanız, tıklatın **Bağlan**.
6. Kimlik bilgilerinizi girerken, oturum hello kullanıcı adı ve parolayla hello 3. adımında belirtilen olun [oluşturma hello web sunucusu VM](#create-web-server-vm) bu makalenin. Merhaba, **Windows Güvenliği** görüntülenen kutusunda hello doğru kimlik bilgilerini listesinde değil, tooclick gerekebilir **daha fazla seçenek**, ardından **farklı bir hesap kullan**, şunları yapabilirsiniz dolayısıyla Merhaba doğru kullanıcı adını ve parolasını belirtin). Tıklatın **Tamam** tooconnect toohello VM.
7. Alırsanız, bir **Uzak Masaüstü Bağlantısı** hello uzak bilgisayarın kimliği Merhaba, doğrulanamıyor, kutusunu bildiren tıklatın **Evet**.
8. Merhaba Internet gelen bağlı toohello MyWebServer VM sunulmuştur. Merhaba Uzak Masaüstü Bağlantısı açık toocomplete hello adımları hello sonraki bölümde bırakın.

Merhaba uzak bağlantı olduğu toohello hello 5. adımında oluşturulan toohello ortak IP adresi kaynak hello portal atanan genel IP adresi [iki alt ağa sahip bir sanal ağ oluşturma](#create-vnet) bu makalenin. Merhaba varsayılan kural hello oluşturduğundan Hello bağlantıya izin veriliyor **MyWebServer nsg** TCP/3389 (RDP) izin verilen NSG gelen tüm kaynak IP adreslerinden gelen toohello VM. Başka bir bağlantı üzerinden tooconnect toohello VM çalışırsanız, ek gelen kuralları toohello NSG izin verme hello ek bağlantı noktalarını eklemedikçe hello bağlantı başarısız.

>[!NOTE]
>Ek gelen kuralları toohello NSG eklerseniz, aynı bağlantı noktalarını hello Windows Güvenlik Duvarı'nı açın ya da bağlantı başarısız hello bu hello emin olun.
>

### <a name="connect-to-internet"></a>Merhaba web sunucusundan VM toohello Internet bağlanılamadı

tooconnect VM, aşağıdaki adımları tam hello hello web sunucusundan giden toohello Internet:

1. MyWebServerVM açık bir uzak bağlantı toohello zaten sahip değilseniz, uzak bağlantı toohello VM hello hello adımları tamamlayarak olun [Bağlan toohello web sunucusundan VM hello Internet](#connect-from-internet) bu makalenin.
2. Merhaba Windows masaüstünden Internet Explorer'ı açın. Merhaba, **Kurulum Internet Explorer 11** iletişim kutusu, tıklatın **önerilen ayarları kullanmayın**, ardından **Tamam**. Bir üretim sunucusu için önerilen ayarları önerilen tooaccept hello olur.
3. Merhaba Internet Explorer Adres çubuğuna girin [aratıp](http:www.bing.com). Bir Internet Explorer iletişim kutusu görüntülenirse, tıklatın **Ekle**, ardından **Ekle** hello içinde **Güvenilen siteler** iletişim kutusu ve tıklatın **Kapat**. Bu işlemi diğer herhangi bir Internet Explorer iletişim kutusu için yineleyin.
4. Merhaba Bing arama sayfası, girin *whatsmyipaddress*, hello Büyüteç düğmesini tıklatın. Bing hello VM oluşturduğunuzda hello portal tarafından oluşturulan hello ortak IP adresi atanmış toohello ortak IP adresi kaynağı döndürür. Merhaba hello ayarlarını incelerseniz **MyWebServer IP** kaynak, gördüğünüz izleyen hello resimde görüldüğü gibi hello toohello ortak IP adresi kaynağı, atanan aynı IP adresi. Başlangıç IP adresi atanmış tooyour VM ancak farklıdır.

    ![Tooweb sunucuya VM](./media/virtual-network-get-started-vnet-subnet/webserver-pip.png)

5.  Merhaba Uzak Masaüstü Bağlantısı açık toocomplete hello adımları hello sonraki bölümde bırakın.

Varsayılan olarak tüm giden bağlantısını hello VM izin olduğundan hello VM gelen mümkün tooconnect toohello Internet değil. Toplama kuralları toohello NSG uygulanır toohello NIC, NIC bağlıysa, toohello alt hello ekleyerek giden bağlantı sınırlayabilirsiniz veya her ikisini de.

Merhaba VM giriş yerleştirirseniz hello hello portalını kullanarak (serbest bırakıldığında) durumu durduruldu, hello genel IP adresi değiştirebilirsiniz. Merhaba ortak IP adresinin hiçbir zaman değişikliği gerekiyorsa (Merhaba varsayılan olan) hello dinamik ayırma yöntemini yerine hello IP adresi için hello statik ayırma yöntemini kullanabilirsiniz. ayırma yöntemleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [IP adresi türleri ve ayırma yöntemleri](virtual-network-ip-addresses-overview-arm.md) makalesi.

### <a name="webserver-to-dbserver"></a>Merhaba web sunucusundan VM toohello veritabanı sunucusu VM bağlanılamadı

VM, aşağıdaki adımları tam hello hello web sunucusundan tooconnect toohello veritabanı sunucusu VM:

1. MyWebServer VM açık bir uzak bağlantı toohello zaten sahip değilseniz, uzak bağlantı toohello VM hello hello adımları tamamlayarak olun [Bağlan toohello web sunucusundan VM hello Internet](#connect-from-internet) bu makalenin.
2. Merhaba Windows Masaüstü hello sol alt köşesindeki Hello Başlat düğmesine tıklayın, sonra yazmaya başlayın *Uzak Masaüstü*. Merhaba Başlat menüsü listesi görüntülendiğinde **Uzak Masaüstü Bağlantısı**, tıklatın.
3. Merhaba, **Uzak Masaüstü Bağlantısı** iletişim kutusunda, girin *DBSunucum* hello bilgisayar adı ve tıklatın **Bağlan**.
4. Merhaba kullanıcı adı ve parolaları hello 3 adımda girdiğiniz girin [oluşturma hello veritabanı sunucusu VM](#create-database-server-vm) bölümünde bu makalede, ardından **Tamam**.
5. Hello uzak bilgisayarın bu hello kimliği doğrulanamıyor bildiren bir iletişim kutusu alırsanız, tıklatın **Evet**.
6. Merhaba Uzak Masaüstü Bağlantısı açık toocomplete hello hello sonraki bölümde adımları tooboth sunucuları bırakın.

Aşağıdaki nedenlerden hello için hello web sunucusu VM mümkün toomake hello bağlantı toohello veritabanı sunucusu VM şunlardır:

- TCP/3389 gelen bağlantıları hello varsayılan NSG hello 5. adımında oluşturulan tüm kaynak IP için etkin [oluşturma hello veritabanı sunucusu VM](#create-database-server-vm) bu makalenin.
- Merhaba web sunucusundan bağlı toohello olan VM hello bağlantıyı başlatan hello veritabanı sunucusu VM olarak aynı sanal ağı. tooconnect tooa bir ortak IP adresi atanmış tooit yok VM, size bağlanması başka bir VM bağlı toohello aynı sanal ağ, VM hello bağlı tooa farklı alt olsa bile.
- Merhaba VM'ler bağlı toodifferent alt ağlar olsa da, Azure alt ağlar arasında bağlantı sağlayacak varsayılan yolların oluşturur. Ancak, kendi oluşturarak hello varsayılan yolların geçersiz kılabilirsiniz. Okuma hello [kullanıcı tanımlı yollar](virtual-networks-udr-overview.md) makale toolearn Azure'da yönlendirme hakkında daha fazla bilgi.

Hello gibi bir uzak bağlantı toohello veritabanı sunucusundan VM hello Internet tooinitiate çalışırsanız [Bağlan toohello web sunucusundan VM hello Internet](#connect-from-internet) bölüm bu makalede, bu hello bkz **Bağlan** seçeneği gri çıkışı. Bağlantı olduğu için hiçbir ortak IP adresi atanmış toohello VM, gelen bağlantıları tooit hello Internet gelen olmayacak şekilde olası gri renkte görüntülenir.

### <a name="connect-toohello-internet-from-hello-database-server-vm"></a>Merhaba veritabanı sunucusundan VM toohello Internet bağlanılamadı

Giden toohello Internet hello aşağıdaki adımları tamamlayarak hello veritabanı sunucusundan VM Bağlan:

1. DBSunucum VM açmak MyWebServer VM hello bir uzaktan bağlantı toohello zaten sahip değilseniz, tam hello hello adımları [hello web sunucusundan VM Bağlan toohello veritabanı sunucusu VM](#webserver-to-dbserver) bu makalenin.
2. Windows masaüstünde hello DBSunucum VM Merhaba, Internet Explorer'ı açın ve adım 2 ve 3'ün hello yaptığınız gibi toohello iletişim kutuları yanıt [toohello Internet hello web sunucusundan VM bağlanmak](#connect-to-internet) bu makalenin.
3. Merhaba adres çubuğunda girin [aratıp](http:www.bing.com).
4. ' I tıklatın **Ekle** hello Internet Explorer iletişim kutusunda görüntülenen, ardından **Ekle**, ardından **Kapat** hello içinde **güvenilen** siteler iletişim kutusu. Ekrana gelen ilave iletişim kutularında bu adımları tamamlayın.
5. Merhaba Bing arama sayfası, girin *whatsmyipaddress*, hello Büyüteç düğmesini tıklatın. Bing hello ortak IP adresi şu anda atanmış toohello VM hello Azure altyapısı tarafından döndürür. 6. Merhaba Uzak Masaüstü toohello DBSunucum VM hello MyWebServer VM gelen kapatın, sonra hello uzak bağlantı toohello MyWebServer VM'yi kapatın.

Varsayılan olarak, tüm giden trafiğe izin verilmediğinden bir ortak IP adresi kaynağı toohello DBSunucum VM atanmamış olsa bile hello giden bağlantı toohello Internet izin verilir. Varsayılan olarak, tüm VM'ler mümkün tooconnect giden toohello Internet'te olan veya olmayan bir ortak IP adresi atanan kaynak toohello VM var. MyWebServer VM, bir ortak IP adresi atanan kaynak mümkün toofor hello edildiği gibi genel IP Internet hello ancak, adres. mümkün tooconnect toohello olmayan.

## <a name="delete-resources"></a>Tüm kaynakları silme

Bu makalede, aşağıdaki adımları tam hello oluşturulan tüm kaynakları toodelete:

1. Bu makalede, tam oluşturulan tooview hello MyRG kaynak grubu içinde hello 1-3 adımları [gözden kaynakları](#review) bu makalenin. Bir kez daha, hello kaynak grubunda hello kaynaklarını gözden geçirin. Önceki adımlar, başına hello MyRG kaynak grubu oluşturduysanız, 4. adımda hello resimde gösterilen hello 12 kaynaklara bakın.
2. Merhaba MyRG dikey penceresinde hello tıklayın **silmek** düğmesi.
3. Merhaba portal tootype hello toodelete istediğiniz hello kaynak grubu tooconfirm adını gerektirir. Kaynakları hello 4 adımda gösterilen hello kaynakları dışında görürseniz [gözden kaynakları](#review) bölüm bu makalede, tıklatın **iptal**. Yalnızca bu makalede bir parçası olarak oluşturulan hello 12 kaynakları görürseniz, yazın *MyRG* hello kaynak grubu adı için ardından **silmek**. Bu nedenle her zaman emin tooconfirm silmeden önce bir kaynak grubu Merhaba içeriğine olması, bir kaynak grubunu silme hello kaynak grubundaki tüm kaynakları siler. Merhaba portal hello kaynak grubu içinde bulunan tüm kaynakları siler ve sonra hello kaynak grubu kendisini siler. Bu işlem birkaç dakika sürer.

## <a name="next-steps"></a>Sonraki adımlar

Bu alıştırmada, bir sanal ağ ve iki VM oluşturdunuz. VM oluşturma esnasında bazı özel ayarlar belirttiniz ve çeşitli varsayılan ayarları kabul ettiniz. Makaleler, üretim sanal ağlar ve sanal makineleri, tüm kullanılabilir ayarlar anlamak tooensure dağıtmadan önce aşağıdaki hello okumanızı öneririz:

- [Sanal ağlar](virtual-networks-overview.md)
- [Genel IP adresleri](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)
- [Ağ arabirimleri](virtual-network-network-interface.md)
- [Ağ güvenlik grupları](virtual-networks-nsg.md)
- [Sanal makineler](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
