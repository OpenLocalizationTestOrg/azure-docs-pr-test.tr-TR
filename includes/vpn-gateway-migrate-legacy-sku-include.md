> [!NOTE]
> * eski bir SKU tooa geçirilirken Hello VPN ağ geçidi genel IP adresini değiştirir yeni SKU.
> * Klasik VPN ağ geçitleri toohello geçiremezsiniz yeni SKU'ları. Merhaba (eski) SKU'ları eski Classic VPN ağ geçitleri can yalnızca kullanın.
> 

Azure VPN boyutlandırılamaz ağ geçitleri arasında eski SKU'ları hello ve hello yeni SKU ailesi. Merhaba hello SKU'ları eski sürümünü kullanarak VPN ağ geçitleri hello Resource Manager dağıtım modelinde varsa, toohello geçirebilirsiniz yeni SKU'ları. toomigrate, sanal ağınız için hello mevcut VPN ağ geçidini silin ve yeni bir tane oluşturun.

Geçiş iş akışı:

1. Tüm bağlantılar toohello sanal ağ geçidi kaldırın.
2. Merhaba eski VPN ağ geçidini silin.
3. Merhaba yeni VPN ağ geçidi oluşturun.
4. Merhaba yeni VPN ağ geçidi IP adresi (siteden siteye bağlantılar için) ile şirket içi VPN cihazlarınızı güncelleştirin.
5. Merhaba ağ geçidi IP adresi toothis ağ geçidi bağlanacak VNet-VNet yerel ağ geçitlerinin değerini güncelleştirin.
6. Bu VPN ağ geçidi üzerinden toohello sanal ağa bağlanma P2S istemciler için yeni istemci VPN yapılandırma paketlerini yükleyin.
7. Merhaba bağlantıları toohello sanal ağ geçidi yeniden oluşturun.
