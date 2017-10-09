## <a name="scenario"></a>Senaryo
toobetter göstermeye nasıl toocreate Nsg'ler, bu belgede hello senaryoyu kullanacaktır.

![VNet senaryosu](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

Bu senaryoda bir NSG hello her alt ağ oluşturacaksınız **TestVNet** aşağıda açıklandığı sanal ağ: 

* **NSG ön uç**. Merhaba ön uç NSG uygulanan toohello olacaktır *ön uç* alt ağı ve iki kural içerir:    
  * **RDP kural**. Bu kural RDP trafiğine toohello sağlayacak *ön uç* alt ağ.
  * **Web kuralı**. Bu kural HTTP trafiği toohello sağlayacak *ön uç* alt ağ.
* **NSG arka uç**. Merhaba arka uç NSG uygulanan toohello olacaktır *arka uç* alt ağı ve iki kural içerir:    
  * **SQL kural**. Bu kural yalnızca hello gelen SQL trafiğe izin veren *ön uç* alt ağ.
  * **Web kuralı**. Bu kural tüm Internet trafiği hello bağlı engellediği *arka uç* alt ağ.

Merhaba bu kurallar birleşimi oluşturma burada hello arka uç alt SQL hello ön uç alt ağından gelen trafiği yalnızca alabilir ve hiçbir erişim toohello hello ön uç alt hello Internet ile iletişim kurabilen sırada Internet sahiptir, DMZ benzeri senaryosu, ve yalnızca gelen HTTP isteklerini alır.

