## <a name="scenario"></a>Senaryo
toobetter göstermeye nasıl toocreate Udr'ler, bu belgede hello senaryoyu kullanacaktır.

![GÖRÜNTÜ AÇIKLAMASI](./media/virtual-network-create-udr-scenario-include/figure1.png)

Bu senaryoda bir UDR hello için oluşturacağınız *ön uç alt* ve hello için başka bir UDR *arka uç alt* , aşağıda açıklandığı gibi: 

* **Ön uç UDR**. Merhaba ön uç UDR uygulanan toohello olacaktır *ön uç* alt ağı ve bir rota içerir:    
  * **RouteToBackend**. Bu rota tüm trafiği toohello arka uç alt toohello göndereceğiniz **FW1** sanal makine.
* **Arka uç UDR**. Merhaba arka uç UDR uygulanan toohello olacaktır *arka uç* alt ağı ve bir rota içerir:    
  * **RouteToFrontend**. Bu rota tüm trafiği toohello ön uç alt toohello göndereceğiniz **FW1** sanal makine.

Bu yolları Hello birleşimi olun bir alt ağ tooanother giden tüm trafiği yönlendirilmiş toohello olacaktır **FW1** sanal gereç olarak kullanılan sanal makine. Bu VM için IP iletimini üzerinde tooturn da gerekir, trafiği alabileceğini tooensure tooother VM'ler hedefleyen.

