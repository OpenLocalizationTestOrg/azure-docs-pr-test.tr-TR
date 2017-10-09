## <a name="scenario"></a>Senaryo
Bir VM tek bir NIC ile oluşturulan ve bağlı tooa sanal ağdır. Merhaba VM gerektirir üç farklı *özel* IP adresleri ve iki *ortak* IP adresleri. Merhaba IP adresleri IP yapılandırmaları aşağıdaki toohello atanır:

* **Ipconfig-1:** atayan bir *statik* özel IP adresi ve bir *statik* genel IP adresi.
* **Ipconfig-2:** atayan bir *statik* özel IP adresi ve bir *statik* genel IP adresi.
* **Ipconfig-3:** atayan bir *statik* özel IP adresi ve ortak IP adresi yok.
  
    ![Birden çok IP adresi](./media/virtual-network-multiple-ip-addresses-scenario/multiple-ipconfigs.png)

Merhaba NIC oluşturulur ve hello NIC olduğunda ekli toohello VM hello VM oluşturulduğunda hello IP ilişkili toohello NIC bağlantılardır. Merhaba hello senaryo için kullanılan IP adresleri için çizim türleridir. İhtiyaç duyduğunuz hangi IP adresi ve atama türleri atayabilirsiniz.

> [!NOTE]
> Merhaba adımları rağmen bu makalenin tüm IP yapılandırmaları tooa atar tek NIC, birden çok IP yapılandırmaları tooany NIC multi-NIC VM içinde de atayabilirsiniz. nasıl toocreate birden çok NIC ile VM okuma toolearn hello [bir VM ile birden çok NIC oluşturma](../articles/virtual-network/virtual-network-deploy-multinic-arm-ps.md) makalesi.
