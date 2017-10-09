---
title: "aaaInfrastructure ve bağlantı tooSAP HANA azure'da (büyük örnekler) | Microsoft Docs"
description: "Gerekli bağlantı altyapı toouse SAP HANA (büyük örnekler) Azure üzerinde yapılandırın."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0af34fbd82413bf63981036a76eaa264d8299ec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-infrastructure-and-connectivity-on-azure"></a>SAP HANA (büyük örnekler) altyapısı ve Azure ile ilgili bağlantı 

Bu kılavuzu okuduktan önce bazı tanımları önceden. İçinde [SAP HANA (büyük örnekler) genel bakış ve Azure ile ilgili mimari](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) ile HANA büyük örneği birimlerin farklı iki sınıf gösterdiğimizi:

- S72, S72m, S144, S144m, S192 ve tooas hello 'ı sınıf türü' adlandırdığımız S192m SKU.
- S384, S384m, S384xm, S576, S768 ve adlandırdığımız S960 tooas SKU ' Type II class' hello.

Merhaba sınıfı tanımlayıcıları hello HANA büyük belge tooeventually başvuran toodifferent özellikleri ve gereksinimleri HANA büyük örneği SKU'larında tabanlı örneği genelinde kullanılan giderek toobe ' dir.

Sık kullandığınız diğer tanımların şunlardır:
- **Büyük örneği damga:** SAP HANA TDI olan bir donanım altyapı yığını sertifikalı ve ayrılmış Azure içindeki toorun SAP HANA örnekleri.
- **SAP HANA azure'da (büyük örnekler):** Azure toorun HANA örneklerinde SAP HANA büyük örneği Damgalar farklı Azure bölgelerinde dağıtılmış donanım sertifikalı TDI hello teklif resmi adı. Merhaba ilgili terim **HANA büyük örneği** azure'da (büyük örnekler) kısaltması SAP HANA ve yaygın olarak kullanılan bu teknik dağıtım kılavuzu.
 

SAP HANA (büyük örnekler) azure'da Hello satın, arasında hello Microsoft Kurumsal hesap ekibi sonlandırıldıktan sonra hello aşağıdaki bilgiler Microsoft toodeploy HANA büyük örneği birimleri tarafından gereklidir:

- Müşteri adı
- İş kişi bilgileri (e-posta adresi ve telefon numarası dahil)
- Teknik kişi bilgileri (e-posta adresi ve telefon numarası dahil)
- Teknik ağ kişi bilgileri (e-posta adresi ve telefon numarası dahil)
- Azure dağıtım bölge (Batı ABD, Doğu ABD, Avustralya Doğu, Avustralya Güneydoğu, Batı Avrupa ve Temmuz itibariyle Kuzey Avrupa 
- 2017)
- SAP HANA Azure (büyük örnekler) SKU (yapılandırma) üzerinde onaylayın
- Zaten hello genel bakış ve mimari belge için dağıtılan her Azure bölgesinin HANA büyük örnekleri için ayrıntılı:
    - / 29 ER P2P bağlantılar, Azure sanal ağlar tooHANA büyük örnekleri bağlanmak için IP adresi aralığı
    - Bir/24 CIDR bloğu hello HANA büyük örnekleri sunucu IP havuzu için kullanılır.
- Başlangıç IP adresi aralığı değerlerini toohello HANA büyük örnekleri bağlayan her Azure vnet'in VNet adres alanı özniteliği Hello kullanılan
- Verileri her HANA büyük örneklerinin sistem için:
  - İstenen ana bilgisayar - tam etki alanı adı ile idealdir.
  - Merhaba HANA büyük örneği birimi hello sunucu IP havuzu adres aralığı - dışında istediğiniz IP adresini hello sunucu IP havuzu adres aralığı içinde HANA büyük örnekleri iç kullanım için ayrılmıştır ilk 30 IP adresleri, hello göz önünde bulundurun
  - SAP HANA SID adı hello SAP HANA örneğinin (gerekli toocreate hello gerekli SAP HANA ilgili disk birimi). Merhaba HANA SID hello izinlerini oluşturmak için gerekli <sidadm> hello NFS birimlerde hangi alma ekli toohello HANA büyük örneği birim. Ayrıca, bağlı hello disk birimlerinin hello adı bileşenlerden biri kullanılır. Merhaba birimi birden fazla HANA örneğinde toorun istiyorsanız, birden çok HANA SID toolist gerekir. Her biri, atanan birimleri ayrı bir kümesini alır.
  - Merhaba GroupID hello hana sidadm kullanıcının sahip hello Linux işletim sistemi gerekli toocreate hello gerekli SAP HANA ilgili disk birimi değil. Merhaba SAP HANA yükleme genellikle 1001 bir grup kimliği ile Merhaba sapsys grubu oluşturur. Merhaba hana sidadm kullanıcı bu grubun parçası olan
  - Merhaba UserID hello hana sidadm kullanıcının sahip hello Linux işletim sistemi gerekli toocreate hello gerekli SAP HANA ilgili disk birimi değil. Birden çok HANA örnekleri hello birim üzerinde çalıştırıyorsanız, tüm hello toolist gerek <sid>adm kullanıcılar 
- Azure abonelik kimliği hello Azure aboneliği toowhich SAP HANA Azure HANA büyük örneklerinde için doğrudan bağlı toobe adımıdır. Bu abonelik kimliği hello toobe ile Merhaba HANA büyük örneği birimlerinin ücret giderek Azure aboneliği başvurur.

Bilgiler, Microsoft hükümleri SAP HANA (büyük örnekler) azure'da hello ve hello bilgi gerekli toolink Azure Vnet tooHANA büyük örnekleri ve tooaccess hello HANA büyük örneği Birimleriniz döndürecektir verdikten sonra.

## <a name="connecting-azure-vms-toohana-large-instances"></a>Azure VM'ler tooHANA büyük örnekleri bağlanma

Zaten belirtilen [SAP HANA (büyük örnekler) genel bakış ve Azure ile ilgili mimari](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) hello en az dağıtımı HANA büyük örnekleri ile Azure görünüyor hello SAP uygulama katmanında ister:

![Azure sanal ağı tooSAP Azure (büyük örnekler) ve şirket içi HANA bağlı](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

Azure VNet yan Hello üzerinde daha yakından baktığınızda, biz hello gereksinimini unutmayın:

- devam eden kullanılan toobe toodeploy hello SAP uygulama katmana hello Vm'leri olan bir Azure sanal Hello tanımı.
- Otomatik olarak, varsayılan alt hello VM'ler içine gerçekten hello bir kullanılan toodeploy olan Azure Vnet tanımlanan hello ağda anlamına gelir.
- Merhaba oluşturulan Azure VNet toohave gereken en az bir VM alt ağı ve bir ExpressRoute ağ geçidi alt ağı. Bu alt hello IP adres aralıklarını belirtilen ve hello aşağıdaki bölümlerde ele olarak atanmalıdır.

Bu nedenle, içine hello Azure VNet oluşturma HANA büyük örnekleri için biraz daha yakın bir göz atalım

### <a name="creating-hello-azure-vnet-for-hana-large-instances"></a>HANA büyük örnekleri için Hello Azure VNet oluşturma

>[!Note]
>Merhaba HANA büyük örneği için Azure VNet hello Azure Resource Manager dağıtım modeli kullanılarak oluşturulmuş olması gerekir. yaygın olarak Klasik dağıtım modeli olarak bilinen hello eski Azure dağıtım modeli, hello HANA büyük örnek çözümü ile desteklenmiyor.

Merhaba VNet hello Azure portal, PowerShell, Azure şablonu veya Azure CLI kullanarak oluşturulabilir (bkz [hello Azure portal kullanarak bir sanal ağ oluşturma](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Aşağıdaki örneğine hello biz hello Azure portal oluşturulan bir VNet içine bakın.

Biz hello Azure Portalı aracılığıyla Azure VNet hello tanımları içine bakarsanız, bakalım hello tanımları ve bazıları ne olanlar toowhat ilişkili biz farklı IP adresi aralıkları listesi. Biz hello hakkında konuşurken gibi **adres alanı**, Azure VNet hello hello adres alanı toouse izin anlama. Bu adres alanı de BGP rota yayma VNet kullanımları hello hello adres aralığıdır. Bu **adres alanı** burada görebilirsiniz:

![Azure VNet, adres alanı hello Azure portalında görüntülenir.](./media/hana-overview-connectivity/image1-azure-vnet-address-space.png)

Merhaba durumda, 10.16.0.0/16 ile önceki hello Azure VNet oldukça büyük ve geniş IP adresi aralığı toouse verildi. Bu VNet içindeki sonraki alt ağlara tüm hello IP adres aralıklarını o 'adres alanı' içinde kendi aralıkları gerektiği anlamına gelir. Genellikle bu tür bir büyük adres aralığı azure'da tek VNet için öneriyoruz değil. Ancak, bir adım ileri alma hello Azure VNet tanımlanan hello alt içine bakalım:

![Azure sanal ağ alt ağları ve kendi IP adres aralıkları](./media/hana-overview-connectivity/image2b-vnet-subnets.png)

Gördüğünüz gibi (burada 'varsayılan' olarak da adlandırılır) ilk VM alt ağı ve 'GatewaySubnet' adlı bir alt ağ ile biz VNet bakın.
Bölümden hello biz 'default' hello grafik olarak çağrıldı hello alt ağın IP adresi aralığını toohello başvuran **Azure VM alt ağ IP adresi aralığı**. Aşağıdaki bölümlerde hello biz toohello IP adres aralığı hello ağ geçidi alt ağı başvurun olarak **VNet ağ geçidi alt ağını IP adresi aralığı**. 

Yukarıdaki Hello iki grafik tarafından gösterilen hello durumda o hello bkz **VNet adres alanı** her ikisini de hello kapsayan **Azure VM alt ağ IP adresi aralığı** ve hello **VNet ağ geçidi alt ağ IP adresi Aralık**. 

Burada tooconserve gerekir veya IP adres aralığı ile belirli diğer durumlarda, hello kısıtlayabilirsiniz **VNet adres alanı** her alt ağı tarafından kullanılan bir VNet toohello belirli bir aralıklarını. Bu durumda, hello tanımlayabilirsiniz **VNet adres alanı** bir VNet gibi birden çok özel aralıkları aşağıda gösterildiği gibi:

![İki alanları ile Azure VNet adres alanı](./media/hana-overview-connectivity/image3-azure-vnet-address-space_alternate.png)

Bu durumda, hello **VNet adres alanı** tanımlanan iki boşluk içeriyor. Bu iki alanlarını aynı toohello IP adres aralıkları için tanımlanan **Azure VM alt ağ IP adresi aralığı** ve hello **VNet ağ geçidi alt ağını IP adresi aralığı.**

İstediğiniz herhangi bir adlandırma standart bu Kiracı alt ağları (VM ağları) için kullanabilirsiniz. Ancak, **ayrıca bir ve sadece bir ağ geçidi alt ağı her VNet için her zaman olmalıdır** toohello SAP HANA (büyük örnekler) Azure expressroute bağlantı hattı üzerinde bağlanır. Ve **bu ağ geçidi alt ağı her zaman "GatewaySubnet" olarak adlandırılmalıdır** tooensure uygun hello ExpressRoute ağ geçidi yerleşimini.

> [!WARNING] 
> Bu hello ağ geçidi alt ağı her zaman "GatewaySubnet." adlı önemlidir

Bitişik olmayan adres aralıklarını bile kullanan birden çok VM alt ağları kullanılabilir. Ancak daha önce belirtildiği gibi bu adres aralıklarını hello tarafından ele alınması gereken **VNet adres alanı** hello VNet toplu halde veya hello listesini tam hello VM alt ağları aralıklarını ve ağ geçidi alt ağı hello.

Merhaba tooHANA büyük örnekleri bağlayan bir Azure sanal hakkında önemli olgu özetleme:

- Toosubmit tooMicrosoft hello gereksinim **VNet adres alanı** HANA büyük örnekleri ilk dağıtımda gerçekleştirirken. 
- Merhaba **VNet adres alanı** hello aralığının Azure VM alt ağ IP adresi aralıklarının ve hello VNet ağ geçidi alt ağı IP adresi aralığını kapsayan tek bir büyük aralık olabilir.
- Veya olarak gönderebilirsiniz **VNet adres alanı** hello farklı IP kapak birden çok aralık adres aralıklarını VM alt ağ IP adresi aralıklarının ve hello VNet ağ geçidi alt ağını IP adresi aralığı.
- tanımlanan hello **VNet adres alanı** kullanılan BGP yönlendirme yayma değil.
- Merhaba ağ geçidi alt ağı Hello adı olması gerekir: **"GatewaySubnet."**
- Merhaba **VNet adres alanı** hello HANA büyük örneği yan tooallow filtre olarak kullanılan veya trafiği toohello HANA büyük örneği Azure birimlerinden vermeyin. Hello BGP yönlendirme bilgilerinin hello Azure VNet ve HANA büyük örneği yan hello üzerinde filtreleme için yapılandırılmış hello IP adres aralıklarını eşleşmiyorsa, bağlantı sorunları ortaya çıkabilir.
- Merhaba ağ geçidi alt ağı ilgili olan bazı ayrıntılar aşağıya 'VNet tooHANA büyük örneği ExpressRoute bağlanma' bölümünde ele alınan vardır



### <a name="different-ip-address-ranges-toobe-defined"></a>Tanımlanan toobe farklı bir IP adresi aralıkları 

Biz zaten hello IP adresi aralıkları gerekli toodeploy HANA büyük örnekleri önceki bölümlerde bazıları sunmuştur. Ancak önemli bazı daha fazla IP adres aralıklarını vardır. Bazı daha ayrıntılı bilgi edelim. Merhaba tüm toobe gereken aşağıdaki IP adresleri tooMicrosoft gereksinim tanımlı, ilk dağıtım için bir istek göndermeden önce toobe gönderildi:

- **VNet adres alanı:** zaten daha önce kullanıma sunulan, veya range(s) atadığınız (veya tooassign planlama) başlangıç IP adresi toohello SAP HANA büyük örneği bağlanma tooyour adres alanı parametresinde hello Azure sanal ağ (VNet) ortam. Bu adres alanı parametre hello Azure VM alt ağı aralıklarının ve hello hello grafik daha önce gösterildiği gibi Azure ağ geçidi alt ağ aralığı oluşan bir çok satırlı değer olduğunu önerilir. Bu aralık, şirket içi veya sunucu IP havuzu veya ER P2P adres aralıkları ile çakışmaması gerekir. Nasıl tooget bu ya da bu IP adresi aralıklarının? Şirket ağı takım ya da hizmet sağlayıcısı, bir veya birden çok IP adresi veya, ağınızda kullanılmaz aralıklarının, sağlamanız gerekir. Örnek: 10.0.1.0/24 (önceki bakın), Azure VM alt ağı olan ve 10.0.2.0/28 (aşağıdaki bakın) Azure ağ geçidi alt ağınızı ise, ardından Azure VNet adres alanı toobe iki satırları önerilir; 10.0.1.0/24 ve 10.0.2.0/28. Merhaba adres alanı değerleri kümelenebilir rağmen toohello alt ağ aralıklarını eşleşen önerilir tooavoid yanlışlıkla yeniden kullanılmasını kullanılmayan IP adresi aralıkları hello gelecekteki büyük adres alanları içinde başka bir yerde ağınızda. **Merhaba VNET adres alanı için ilk dağıtımda isterken hangi gereksinimlerini toobe tooMicrosoft gönderilen bir IP adresi aralığı olan**

- **Azure VM alt ağ IP adresi aralığı:** zaten daha önce açıklandığı gibi bu IP adresi aralığı, atadığınız (veya tooassign planlama) hello biri olan toohello Azure sanal alt ağ toohello SAP HANA büyük örneği ortamı bağlanma Azure sanal parametresinde . Bu IP adresi aralığı kullanılan tooassign IP adreslerini tooyour Azure VM'ler ' dir. Bu aralık dışında Hello IP adreslerini tooconnect tooyour SAP HANA büyük örneği sunucuları izin verilir. Gerekirse, birden çok Azure VM alt ağı kullanılabilir. A/24 CIDR bloğu, Microsoft tarafından her Azure VM alt ağı için önerilir. Bu adres aralığı hello Azure VNet adres alanı kullanılan hello değerlerin bir parçası olması gerekir. Nasıl tooget bu IP adresi aralığı? Şirket ağı takım ya da hizmet sağlayıcısı, ağınızda kullanılan olmayan bir IP adresi aralığı sağlamalıdır.

- **Sanal ağ geçidi alt ağını IP adresi aralığı:** boyutu olacaktır planladığınız toouse, hello özellikleri bağlı olarak hello önerilir:
   - Çok yüksek performanslı ExpressRoute ağ geçidi: / 26 adres bloğu - SKU'ları türü II sınıfı için gerekli
   - VPN ve yüksek performanslı ExpressRoute ağ geçidi kullanarak ExpressRoute ile birlikte bulunma (veya daha küçük): / 27 adres bloğu
   - Diğer durumlarda: / 28 adres bloğu. Bu adres aralığı hello "VNet adres alanı" değerlerde kullanılan hello değerlerin bir parçası olması gerekir. Bu adres aralığı toosubmit tooMicrosoft gerektiğini hello Azure VNet adres alanı değerleri kullanılan hello değerlerin bir parçası olması gerekir. Nasıl tooget bu IP adresi aralığı? Şirket ağı takım ya da hizmet sağlayıcısı, ağınızda kullanılan olmayan bir IP adresi aralığı sağlamalıdır. 

- **Adres aralığı ER P2P bağlantısını:** bu aralığın başlangıç IP SAP HANA büyük örneği ExpressRoute (ER) P2P bağlantınızı arasındadır. Bu IP adresi aralığı/29 olmalıdır CIDR IP adresi aralığı. Bu aralık, şirket içi veya başka bir Azure IP adres aralıklarını çakışmaması gerekir. Bu IP adresi aralığı Azure VNet ExpressRoute ağ geçidi toohello SAP HANA büyük örneği sunucularınızdan hello ER bağlantı kurma kullanılan tooset ' dir. Nasıl tooget bu IP adresi aralığı? Şirket ağı takım ya da hizmet sağlayıcısı, ağınızda kullanılan olmayan bir IP adresi aralığı sağlamalıdır. **Bu aralığı ilk bir dağıtım için isterken hangi gereksinimlerini toobe tooMicrosoft gönderilen bir IP adresi aralığı**
  
- **Sunucu IP havuzu adres aralığı:** kullanılan tooassign hello tek tek IP adresi tooHANA büyük örnek sunucuları bu IP adresi aralığı değil. Merhaba önerilir alt ağ boyutu bir/24 CIDR engelle -, ancak olabilir küçük tooa en az 64 IP adresleri sağlama. Bu aralıktan hello ilk 30 IP adreslerini kullanmak için Microsoft tarafından ayrılır. Bu olay için hello aralığının hello boyutu seçerken eklendiğinden emin olun. Bu aralık, şirket içi veya başka bir Azure IP adresleri çakışmaması gerekir. Nasıl tooget bu IP adresi aralığı? Şirket ağı takım ya da hizmet sağlayıcısı, ağınızda kullanılan olmayan bir IP adresi aralığı sağlamalıdır. Bir/24 (benzersiz CIDR önerilir) hello SAP HANA azure'da (büyük örnekler) için gereken belirli IP adresleri atamak için kullanılan toobe engelleyin. **Bu aralığı ilk bir dağıtım için isterken hangi gereksinimlerini toobe tooMicrosoft gönderilen bir IP adresi aralığı**
 
Toodefine gerekir ve başlangıç IP adresi aralıklarını yukarıdaki planı olsa, bunları tüm aktarılan toobe tooMicrosoft gerekir. toosummarize hello yukarıdaki gerekli tooname tooMicrosoft olduğunuz hello IP adres aralıklarını şunlardır:

- Azure sanal ağ adres alanları
- ER P2P bağlantı adres aralığı
- Sunucu IP havuzu adres aralığı

Gerektirir tooconnect tooHANA büyük örnekleri gereken ek sanal ağlar ekleme toosubmit hello tooMicrosoft ekleyeceğiniz yeni Azure VNet adres alanı. 

Tooconfigure gerekir ve sonunda tooMicrosoft sağlamak gibi hello farklı aralıkları ve bazı örnek aralıkları örneği aşağıdadır. Gördüğünüz gibi hello Azure VNet adres alanı için hello değer hello ilk örnekte toplanmaz ancak hello ilk Azure VM alt ağ IP adresi aralığı ve hello VNet ağ geçidi alt ağını IP adresi aralığı hello aralığından tanımlanmadı. İş uygun şekilde yapılandırma ve gönderme ek IP hello hello Azure VNet içinde birden fazla VM alt ağları kullanarak adres aralıklarını hello Azure VNet adres alanı bir parçası olarak ek VM alt ağı hello.

![SAP HANA Azure (büyük örnekler) en az dağıtımı için gerekli IP adresi aralıkları](./media/hana-overview-connectivity/image4b-ip-addres-ranges-necessary.png)

Ayrıca tooMicrosoft gönderme hello verileri toplama hello olanağına sahip olursunuz. Bu durumda, hello hello Azure VNet adres alanı yalnızca tek bir boşluk içerir. Başlangıç IP adresi aralıklarını Hello örnek daha önce kullanılan kullanma. Bu toplu VNet adres alanı gibi görünebilir:

![SAP HANA Azure (büyük örnekler) en az dağıtımı için gerekli IP adresi aralıklarını ikinci olasılığı](./media/hana-overview-connectivity/image5b-ip-addres-ranges-necessary-one-value.png)

Hello Azure VNet adres alanı hello tanımlanan iki küçük aralıkları yerine yukarıda gördüğünüz gibi 4096 IP adreslerini kapsayan tek bir büyük aralık sunuyoruz. Merhaba adres alanı, büyük tanımı bazı yerine büyük aralıkları kullanılmayan bırakır. Hello VNet adres alanı değerleri BGP rota yayılması için kullanıldığından, kullanımını kullanılmayan aralıkları şirket içi hello veya ağınızdaki başka bir yerde yönlendirme sorunlara neden olabilir. Bu nedenle bu adres alanı sıkı bir şekilde kullanılan hello gerçek alt ağ adres alanıyla hizalı önerilen tookeep hello olur. Kapalı kalma süresi hello Vnet'in üzerinde yansıtılmasını olmadan gerekirse, her zaman yeni adres alanı değerleri daha sonra ekleyebilirsiniz.
 
> [!IMPORTANT] 
> Her IP adresi aralığı, ER-P2P, sunucu IP havuzuna, Azure VNet adres alanı gerekir **değil** birbirleri ile üst üste veya başka bir aralığı ağınızdaki başka bir yerde kullanılan; her ayrık olmalıdır ve hello iki grafik olarak önceki Göster olmayabilir bir alt ağdan başka bir aralığı. Aralıkları arasında çakışmalar meydana gelirse, hello Azure VNet toohello expressroute bağlantı hattı bağlanamayabilir.

### <a name="next-steps-after-address-ranges-have-been-defined"></a>Adres aralıklarını tanımlanan sonraki adımlar
Başlangıç IP adresi aralıklarını tanımlandıktan sonra hello aşağıdaki etkinlikleri toohappen gerekir:

1. Başlangıç IP adresi aralıklarını hello hello belgenin başında listelenen diğer verileri birlikte Azure VNet adres alanı, hello ER P2P bağlantısını ve sunucu IP havuzu adres aralığı, gönderin. Bu anda, toocreate hello VNet ve hello VM alt ağları başlatmak da. 
2. Hızlı rota devresi, Azure aboneliği ile Merhaba HANA büyük örneği damga arasında Microsoft tarafından oluşturulur.
3. Bir kiracı ağı hello büyük örneği damgası Microsoft tarafından oluşturulur.
4. Microsoft Azure (büyük örnekler) altyapısı tooaccept üzerinde SAP HANA hello Azure VNet adres iletişim kuran alanınızı HANA büyük örneğiyle IP adreslerinden ağ iletişimi yapılandırır.
5. Merhaba, Azure (büyük örnekler) SKU üzerinde belirli SAP HANA satın bağlı olarak bir işlem birimi bir kiracı ağı içinde Microsoft atar, ayırmak ve depolama bağlayın ve hello işletim sistemini (SUSE veya Red Hat Linux) yükleyin. Bu birimleri için IP adresleri sunucu IP havuzu adres aralığı tooMicrosoft gönderilen hello dışında alınır.

Merhaba dağıtım işleminin Hello sonunda, Microsoft Veri tooyou aşağıdaki hello sunar:
- Azure sanal ağlar tooHANA büyük örnekleri bağlanır, Azure VNet(s) toohello expressroute bağlantı hattı tooconnect gerekli bilgiler:
     - Yetkilendirme anahtarları
     - ExpressRoute PeerID
- Veri tooaccess HANA büyük örnekleri çalıştırdıktan sonra expressroute bağlantı hattı ve Azure VNet kurdu.

Merhaba belgede HANA büyük örnekleri bağlayan hello dizisi bulabileceğiniz [tooEnd SAP HANA büyük örnekleri için Kurulum sona](https://azure.microsoft.com/resources/sap-hana-on-azure-large-instances-setup/). Aşağıdaki adımları hello çoğunu bu belgedeki örnek bir dağıtım gösterilir. 


## <a name="connecting-a-vnet-toohana-large-instance-expressroute"></a>VNet tooHANA büyük örneği ExpressRoute bağlanma

Tüm hello IP adres aralıklarını tanımlanan ve şimdi hello verileri Microsoft'tan aldım gibi hello büyük örnekleri tooHANA önce oluşturulan VNet bağlanma başlatabilirsiniz. Bir kez hello Azure VNet oluşturulur, bir ExpressRoute ağ geçidi hello VNet toolink hello VNet toohello toohello müşteri Kiracı hello büyük örneği damgasında bağlayan expressroute bağlantı hattı üzerinde oluşturulmuş olması gerekir.

> [!NOTE] 
> Bu adım too30 dakika toocomplete hello yeni ağ geçidi Azure aboneliği belirlenmiş hello oluşturulur ve ardından Azure VNet bağlı toohello belirtilen devam edebilir.

Bir ağ geçidi zaten varsa, onu bir ExpressRoute ağ geçidi olup olmadığını denetleyin. Yoksa, hello ağ geçidi silinmiş ve bir ExpressRoute ağ geçidi yeniden. Azure VNet zaten hello toohello expressroute bağlantı hattı için şirket içi bağlantı bağlandığınızdan bu yana bir ExpressRoute ağ geçidi zaten, kurulamazsa, toohello sanal ağlara bağlama bölümüne geçin.

- Her iki hello (yeni) kullanmak [Azure portal](https://portal.azure.com/), veya PowerShell toocreate ExpressRoute VPN ağ geçidi tooyour VNet bağlı.
  - Hello Azure portal kullanacaksanız, yeni bir ekleyin **sanal ağ geçidi** ve ardından **ExpressRoute** hello ağ geçidi türü.
  - Bunun yerine PowerShell seçerseniz, ilk indirme ve hello son kullanma [Azure PowerShell SDK](https://azure.microsoft.com/downloads/) tooensure en iyi bir deneyim. Aşağıdaki komutları hello bir ExpressRoute ağ geçidi oluşturun. Merhaba metinleri öncesinde tarafından bir  _$_  belirli bilgilerle güncelleştirilmemiş bu gereksinimi toobe kullanıcı tanımlı değişkenlerdir.

```PowerShell
# These Values should already exist, update toomatch your environment
$myAzureRegion = "eastus"
$myGroupName = "SAP-East-Coast"
$myVNetName = "VNet01"

# These values are used toocreate hello gateway, update for how you wish hello GW components toobe named
$myGWName = "VNet01GW"
$myGWConfig = "VNet01GWConfig"
$myGWPIPName = "VNet01GWPIP"
$myGWSku = "HighPerformance" # Supported values for HANA Large Instances are: HighPerformance or UltraPerformance

# These Commands create hello Public IP and ExpressRoute Gateway
$vnet = Get-AzureRmVirtualNetwork -Name $myVNetName -ResourceGroupName $myGroupName
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
New-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName `
-Location $myAzureRegion -AllocationMethod Dynamic
$gwpip = Get-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $myGWConfig -SubnetId $subnet.Id `
-PublicIpAddressId $gwpip.Id

New-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName -Location $myAzureRegion `
-IpConfigurations $gwipconfig -GatewayType ExpressRoute `
-GatewaySku $myGWSku -VpnType PolicyBased -EnableBgp $true
```

Bu örnekte, hello HighPerformance ağ geçidi SKU'su kullanıldı. SAP HANA azure'da (büyük örnekler) için desteklenen ağ geçidi SKU hello gibi HighPerformance veya UltraPerformance Seçenekleriniz şunlardır.

> [!IMPORTANT]
> İçin HANA büyük hello SKU örneklerini türleri S384, S384m, S384xm, S576, S768 ve S960 (II sınıfı SKU'ları türü), hello hello UltraPerformance ağ geçidi SKU'su kullanımını zorunludur.

### <a name="linking-vnets"></a>Sanal ağları bağlama

Hello Azure VNet sahip bir ExpressRoute ağ geçidi, bu bağlantı için oluşturulan (büyük örnekler) Azure expressroute bağlantı hattı'de Microsoft tooconnect hello ExpressRoute ağ geçidi toohello SAP HANA tarafından sağlanan hello yetkilendirme bilgileri kullanın. Bu adım, hello Azure portal veya PowerShell kullanılarak gerçekleştirilebilir. Merhaba portal önerilir ancak PowerShell yönergeleri aşağıdaki gibidir. 

- Her bağlantı için farklı bir AuthGUID kullanarak her sanal ağ geçidi için komutları aşağıdaki hello yürütün. Microsoft tarafından sağlanan hello bilgilerinden hello ilk iki girişleri Hello betik aşağıda gösterildiği gelir. Ayrıca, hello AuthGUID her VNet ve alt ağ geçidi için özeldir. Başka bir Azure sanal tooadd istiyorsanız, tooget başka bir AuthID HANA büyük örnekleri Azure'a bağlanır, expressroute bağlantı hattı için gereksinim duyduğunuz gelir. 

```PowerShell
# Populate with information provided by Microsoft Onboarding team
$PeerID = "/subscriptions/9cb43037-9195-4420-a798-f87681a0e380/resourceGroups/Customer-USE-Circuits/providers/Microsoft.Network/expressRouteCircuits/Customer-USE01"
$AuthGUID = "76d40466-c458-4d14-adcf-3d1b56d1cd61"

# Your ExpressRoute Gateway Information
$myGroupName = "SAP-East-Coast"
$myGWName = "VNet01GW"
$myGWLocation = "East US"

# Define hello name for your connection
$myConnectionName = "VNet01GWConnection"

# Create a new connection between hello ER Circuit and your Gateway using hello Authorization
$gw = Get-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName
    
New-AzureRmVirtualNetworkGatewayConnection -Name $myConnectionName `
-ResourceGroupName $myGroupName -Location $myGWLocation -VirtualNetworkGateway1 $gw `
-PeerId $PeerID -ConnectionType ExpressRoute -AuthorizationKey $AuthGUID
```

Aboneliğinizle ilişkili tooconnect hello ağ geçidi toomultiple ExpressRoute bağlantı hatları istiyorsanız, bu adımı tooexecute birden çok kez gerekebilir. Örneğin, büyük olasılıkla adımıdır tooconnect hello hello VNet tooyour şirket içi ağ bağlanır aynı Vnet'e ağ geçidi toohello expressroute bağlantı hattı.

## <a name="adding-more-ip-addresses-or-subnets"></a>Daha fazla IP adresleri veya alt ekleme

Daha fazla IP adresleri veya alt eklerken ya da hello Azure portal, PowerShell veya CLI kullanın.

Bu durumda, hello tooadd hello yeni IP adresi aralığı yeni aralık toohello VNet adres alanı yeni bir birleşik aralık üretmek yerine önerilir. Her iki durumda da toosubmit bu değişiklik tooMicrosoft tooallow bu yeni IP adresi aralığı toohello HANA büyük örneği birimleri dışında istemci olması gerekir. Eklenen Azure destek isteği tooget hello yeni VNet adres alanı açabilirsiniz. Onay aldıktan sonra hello sonraki adımları gerçekleştirin.

toocreate ek bir alt ağ hello Azure portalı üzerinden hello makaleye bakın [hello Azure portal kullanarak bir sanal ağ oluşturma](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ve PowerShell üzerinden toocreate [PowerShellkullanarakbirsanalağoluşturma](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="adding-vnets"></a>Sanal ağlar ekleme

Bir veya daha fazla Azure Vnet başlangıçta bağladıktan sonra Azure (büyük örnekler) üzerinde SAP HANA'ya erişmek ek olanları tooadd isteyebilirsiniz. İlk olarak, bir Azure destek isteği göndermek, hem hello belirli bilgiler tanımlayıcı hello belirli Azure dağıtım hem de başlangıç IP adresi alanı aralıklarının hello Azure VNet adres alanı, bu istekte içerir. SAP HANA Azure hizmet yönetimi üzerinde daha sonra tooconnect ihtiyacınız hello gerekli bilgileri sağlar ek sanal ağlar ve ExpressRoute hello. Her sanal ağ için benzersiz bir yetkilendirme anahtar tooconnect toohello expressroute bağlantı hattı tooHANA büyük örnekleri gerekir.

Adımları tooadd yeni Azure VNet:

1. Merhaba bkz tamamlamak hello ekleme işleminin ilk adımında hello _Azure VNet oluşturma_ bölümü.
2. Hello bkz tamamlamak hello ekleme işleminde ikinci adım hello _ağ geçidi alt ağı oluşturma_ bölümü.
3. tooconnect ek sanal ağlar toohello HANA büyük örneği expressroute bağlantı hattı, açmanıza Azure destek isteği bilgilerle yeni VNet hello ve yeni bir yetkilendirme anahtar isteyin.
4. Merhaba yetkilendirme olduğunu tamamlamak için toocomplete hello üçüncü adım hello ekleme işleminde hello Microsoft tarafından sağlanan yetkilendirme bilgilerini kullanın bildirim sonra hello bakın _sanal ağlara bağlama_ bölümü.

## <a name="increasing-expressroute-circuit-bandwidth"></a>ExpressRoute bağlantı hattı bant genişliğini artırma

SAP HANA Azure Hizmet Yönetimi başvurun. Tavsiye edilir tooincrease hello bant genişliği (büyük örnekler) Azure expressroute bağlantı hattı üzerinde hello SAP HANA varsa, Azure destek isteği oluşturun. (Tek hattı bant genişliği tooa en fazla 10 GB/sn yukarı artış isteğinde bulunabilirsiniz.) Merhaba işlemi tamamlandıktan sonra sonra bildirim alırsınız; ek eylem tooenable bu daha yüksek hız Azure gerekmiyor.

## <a name="adding-an-additional-expressroute-circuit"></a>Ek bir expressroute bağlantı hattı ekleme

Ek bir expressroute, Azure destek isteği toocreate bir yeni expressroute bağlantı hattı (ve tooget yetkilendirme bilgileri tooconnect tooit) olması gerektiğini önerilir, Azure Hizmet Yönetimi, SAP HANA başvurun. gittiği hello adres alanı sanal ağlar Azure Hizmet Yönetimi tooprovide yetkilendirme üzerinde SAP HANA sırada hello isteği yapmadan önce tanımlanmalıdır hello kullanılabilir.

Merhaba yeni hattı oluşturup hello SAP HANA Azure Hizmet Yönetimi Yapılandırma tamamlandıktan sonra tooreceive bildirim tooproceed ihtiyacınız hello bilgilerle adımıdır. Yukarıdaki oluşturmak ve hello yeni VNet toothis ek hattı bağlanmak için sağlanan hello adımları izleyin. Zaten tooanother SAP HANA Merhaba, Azure (büyük örneği) expressroute bağlantı hattı üzerinde bağlıysa, mümkün tooconnect Azure Vnet toothis ek hattı olmayan aynı Azure bölgesi.

## <a name="deleting-a-subnet"></a>Bir alt ağı silme

tooremove bir sanal alt ya da hello Azure portal, PowerShell veya CLI kullanılabilir. Azure sanal ağ IP adresi aralığı/Azure VNet adres alanı bir toplanmış aralığı olduğu durumda, Microsoft ile sizin için hiçbir izleme yoktur. Bu hello dışında VNet hala silinmiş hello alt içerir BGP rota adres alanı yayılıyor. Hello Azure sanal ağ IP adresi aralığı/Azure VNet adres alanı birden çok IP adres aralığı tanımlanmışsa hangisinin silinmiş atanan tooyour alt ağ, VNet adres alanınızı dışında silin ve daha sonra Azure Hizmet Yönetimi SAP HANA bildirin. Merhaba buradan, SAP HANA (büyük örnekler) azure'da aralıkları tooremove ile toocommunicate izin verilir.

Alt ağları kaldırma belirli, ayrılmış Azure.com Kılavuzu, alt ağları kaldırma hello işlemdir henüz olmasa hello ters hello işleminin bunları eklemek için. Merhaba makalesine bakın [hello Azure portal kullanarak bir sanal ağ oluşturma](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) alt ağları oluşturma hakkında daha fazla bilgi için.

## <a name="deleting-a-vnet"></a>Bir sanal ağı silme

Bir VNet silerken ya da hello Azure portal, PowerShell veya CLI kullanın. SAP HANA Azure Hizmet Yönetimi hello varolan yetkilerini hello SAP HANA Azure (büyük örnekler) expressroute bağlantı hattı üzerinde üzerinde kaldırır ve hello Azure sanal ağ IP adresi aralığı/Azure VNet adres alanıyla hello iletişimi için HANA büyük örnekleri kaldırın.

Merhaba VNet kaldırıldıktan sonra range(s) toobe kaldırılmış bir Azure destek isteği tooprovide hello IP adres alanını açın.

Sanal ağlar kaldırma belirli, ayrılmış Azure.com Kılavuzu, sanal ağlar kaldırmak için hello işlemdir henüz olmasa hello ters hello işleminin, yukarıda açıklanan eklemek için. Merhaba makalelerine bakın [hello Azure portal kullanarak bir sanal ağ oluşturma](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ve [PowerShell kullanarak bir sanal ağ oluşturma](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) sanal ağlar oluşturma hakkında daha fazla bilgi için.

her şeyi kaldırılır, tooensure aşağıdaki öğelerindeki hello Sil:

- ExpressRoute bağlantısı, sanal ağ geçidi hello VNet ağ geçidi genel IP ve sanal ağ

## <a name="deleting-an-expressroute-circuit"></a>Bir expressroute bağlantı hattı silme

tooremove (büyük örnekler) Azure expressroute bağlantı hattı üzerinde ek bir SAP HANA SAP HANA Azure Hizmet Yönetimi ile bir Azure destek isteği açın ve hello hattı silinip silinmediğini isteyin. Hello Azure aboneliği silebilir veya hello gerektiği VNet tutun. Ancak, hello HANA büyük örnekleri expressroute bağlantı hattı arasında hello bağlantı silmeniz gerekir ve sanal ağ geçidi hello bağlanır.

Ayrıca tooremove VNet istiyorsanız, bir VNet yukarıdaki hello bölümdeki silme hello yönergeleri izleyin.


