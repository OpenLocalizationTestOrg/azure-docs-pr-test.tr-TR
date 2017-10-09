> [!div class="op_single_selector"]
> * [Portal](../articles/virtual-network/virtual-network-multiple-ip-addresses-portal.md)
> * [PowerShell](../articles/virtual-network/virtual-network-multiple-ip-addresses-powershell.md)
> * [CLI 2.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli.md)
> * [CLI 1.0](../articles/virtual-network/virtual-network-multiple-ip-addresses-cli-nodejs.md)
> * [Şablon](../articles/virtual-network/virtual-network-multiple-ip-addresses-template.md)
>

Bir Azure sanal makine (VM) bağlı bir veya daha fazla ağ arabirimleri (NIC) tooit. Bir NIC'e sahip olabilir veya atanan tooit daha statik veya dinamik ortak ve özel IP adresleri. Birden çok IP adresleri tooa VM hello aşağıdaki özellikleri sağlar:

* Tek bir sunucuda farklı IP adreslerine ve SSL sertifikalarına sahip birden fazla web sitesi veya hizmetin barındırılması.
* Güvenlik duvarı veya yük dengeleyici gibi bir sanal ağ gereci olarak görev yapma.
* herhangi bir hello özel IP adresleri herhangi bir hello NIC'ler tooan Azure yük dengeleyici arka uç havuzu için yeteneği tooadd hello. Geçmiş, yalnızca hello hello birincil NIC olabilir hello için birincil IP adresi tooa arka uç havuzu eklenen. hakkında daha fazla bilgi toolearn tooload dengelemek nasıl birden fazla IP yapılandırması hello okuma [Yük Dengeleme birden fazla IP yapılandırması](../articles/load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi.

Her bağlı NIC tooa VM bir veya daha fazla IP yapılandırmaları tooit ilişkilendirilmiş. Her yapılandırmaya bir statik veya dinamik özel IP adresi atanır. Her yapılandırma bir ortak IP adresi ilişkili kaynak tooit da sahip olabilirsiniz. Genel bir IP adresi kaynağı ya da bir dinamik veya statik genel IP adresi atanmış tooit sahiptir. IP hakkında daha fazla toolearn adresleri Azure'da, hello okuma [azure'daki IP adresleri](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) makalesi. 

Birçok özel IP sınırı toohow olan adresleri tooa NIC atanabilir Bir Azure aboneliği kullanılan birçok ortak IP adresleri sınırı toohow bulunmaktadır. Merhaba bkz [Azure sınırlar](../articles/azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) Ayrıntılar için makale.
