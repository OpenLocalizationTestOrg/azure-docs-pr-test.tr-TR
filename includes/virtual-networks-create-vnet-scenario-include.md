## <a name="scenario"></a>Senaryo
toobetter göstermeye toocreate VNet ve alt ağlar, bu belgenin nasıl kullanacağını hello senaryo aşağıdaki.

![VNet senaryosu](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

Bu senaryoda, **192.168.0.0./16** bloğuna ayrılmış CIDR bulunan **TestVNet** adıyla bir VNet oluşturacaksınız. Vnet'inizi alt ağlar aşağıdaki hello içerir: 

* CIDR bloğu olarak **192.168.1.0/24** kullanan **Ön Uç**.
* CIDR bloğu olarak **192.168.2.0/24** kullanan **rka Uç**.

