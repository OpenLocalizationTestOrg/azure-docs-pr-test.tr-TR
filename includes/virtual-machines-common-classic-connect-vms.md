

![Sanal makinelerde tek başına bulut hizmeti](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

Bir sanal ağ, sanal makineleriniz yerleştirirseniz toouse için istediğiniz kaç bulut Hizmetleri Yük Dengeleme ve kullanılabilirlik kümeleri karar verebilirsiniz. Ayrıca, hello sanal makineleri düzenleyebilirsiniz hello ağlardaki aynı şekilde şirket içi ağ ve hello sanal ağ tooyour bağlanın ağ şirket. Örnek aşağıda verilmiştir:

![Bir sanal ağdaki sanal makineler](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

Azure'da yolu tooconnect sanal makineler önerilen hello sanal ağlardır. Merhaba en iyi uygulama her katman ayrı bulut hizmetinde, uygulamanızın tooconfigure olduğu. Ancak, bazı sanal makineler toocombine gerekebilir farklı uygulama katmanlarındaki hello içine hizmet tooremain hello en fazla abonelik başına 200 bulut Hizmetleri içinde aynı bulut. Bu ve diğer sınırları tooreview bkz [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../articles/azure-subscription-service-limits.md).

## <a name="connect-vms-in-a-virtual-network"></a>Sanal makineleri sanal bir ağa bağlan
bir sanal ağdaki sanal makinelerden tooconnect:

1. Hello Hello sanal ağ oluşturma [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) ve 'Klasik dağıtım' belirtin.
2. Tasarımınız kullanılabilirlik kümeleri için dağıtım tooreflect için bulut hizmetlerini Hello kümesi oluşturun ve Yük Dengeleme. Hello Azure portal'ı tıklatın **yeni > işlem > bulut hizmeti** her bir bulut hizmeti için.

  Merhaba bulut hizmetinin ayrıntılarını dolgu olarak seçin aynı hello _kaynak grubu_ hello sanal ağ ile kullanılır.

3. toocreate her yeni sanal makine, tıklatın **yeni > işlem**, hello uygun VM görüntüsünü seçin hello sonra **öne çıkan uygulamalar**.

  Merhaba VM içinde **Temelleri** dikey penceresinde, seçin aynı hello _kaynak grubu_ hello sanal ağ ile kullanılır.

  ![Bir sanal ağ kullanırken VM temel bilgileri dikey penceresi](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. VM hello dolgu olarak **ayarları**, doğru hello seçin _bulut hizmeti_ veya _sanal ağ_ hello VM için.

  Azure öğesi seçiminize göre hello diğer seçer.

  ![Bir sanal ağ kullanırken VM ayarlar dikey penceresi](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a>Sanal makineleri bir tek başına bulut hizmetine bağlanmak
tooconnect sanal makinelerde tek başına bulut hizmeti:

1. Hello Hello bulut hizmeti Oluştur [Azure portal](http://portal.azure.com). Tıklatın **yeni > işlem > bulut hizmeti**. Veya, ilk sanal makine oluşturduğunuzda, dağıtımınız için hello bulut hizmeti oluşturabilir.
2. Merhaba sanal makineleri oluştururken hello bulut hizmetiyle aynı kaynak grubunda kullanılan hello seçin.

  ![Bir sanal makine tooan mevcut bulut hizmeti Ekle](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  Merhaba VM ayrıntılarını doldukça hello hello ilk adımda oluşturduğunuz bulut hizmeti adını seçin.

  ![Bir sanal makine için bir bulut hizmeti seçme](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
