## <a name="scenario"></a><span data-ttu-id="0ded5-101">Senaryo</span><span class="sxs-lookup"><span data-stu-id="0ded5-101">Scenario</span></span>
<span data-ttu-id="0ded5-102">toobetter göstermeye toocreate VNet ve alt ağlar, bu belgenin nasıl kullanacağını hello senaryo aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="0ded5-102">toobetter illustrate how toocreate a VNet and subnets, this document will use hello scenario below.</span></span>

![VNet senaryosu](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="0ded5-104">Bu senaryoda, **192.168.0.0./16** bloğuna ayrılmış CIDR bulunan **TestVNet** adıyla bir VNet oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0ded5-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="0ded5-105">Vnet'inizi alt ağlar aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="0ded5-105">Your VNet will contain hello following subnets:</span></span> 

* <span data-ttu-id="0ded5-106">CIDR bloğu olarak **192.168.1.0/24** kullanan **Ön Uç**.</span><span class="sxs-lookup"><span data-stu-id="0ded5-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="0ded5-107">CIDR bloğu olarak **192.168.2.0/24** kullanan **rka Uç**.</span><span class="sxs-lookup"><span data-stu-id="0ded5-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

