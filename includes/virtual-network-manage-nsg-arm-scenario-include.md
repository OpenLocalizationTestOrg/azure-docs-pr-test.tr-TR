## <a name="sample-scenario"></a>Örnek senaryo
toobetter göstermeye toomanage Nsg'ler, bu makalede hello senaryo aşağıdaki nasıl kullanır.

![VNet senaryosu](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

Bu senaryoda bir NSG hello her alt ağ oluşturacaksınız **TestVNet** aşağıda açıklandığı sanal ağ: 

* **NSG ön uç**. Merhaba ön uç NSG uygulanan toohello olacaktır *ön uç* alt ağı ve iki kural içerir:    
  * **RDP kural**. Bu kural RDP trafiğine toohello sağlayacak *ön uç* alt ağ.
  * **Web kuralı**. Bu kural HTTP trafiği toohello sağlayacak *ön uç* alt ağ.
* **NSG arka uç**. Merhaba arka uç NSG uygulanan toohello olacaktır *arka uç* alt ağı ve iki kural içerir:    
  * **SQL kural**. Bu kural yalnızca hello gelen SQL trafiğe izin veren *ön uç* alt ağ.
  * **Web kuralı**. Bu kural tüm Internet trafiği hello bağlı engellediği *arka uç* alt ağ.

Bu kurallar Hello birleşimi oluşturma burada hello arka uç alt hello ön uç alt ağından gelen trafiği SQL trafik için yalnızca alabilir ve hello ön uç alt hello ile iletişim kurabilen sırada hiçbir erişim toohello Internet sahip bir DMZ benzer senaryo Internet ve yalnızca gelen HTTP isteklerini alacak.

Yukarıda açıklanan toodeploy hello senaryosu izleyin [bu bağlantıyı](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), tıklatın **tooAzure dağıtmak**hello varsayılan parametre değerlerini gerekiyorsa değiştirin ve hello hello Portalı'ndaki yönergeleri izleyin. Merhaba örnek yönergeleri aşağıda hello şablonu kullanılan toodeploy bir kaynak grubu adları içindeydi **RG NSG**. 

