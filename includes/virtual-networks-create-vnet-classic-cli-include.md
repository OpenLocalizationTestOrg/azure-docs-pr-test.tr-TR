## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>Nasıl toocreate Azure CLI kullanarak Klasik VNet
Windows, Linux veya OSX çalıştıran herhangi bir bilgisayardan hello komut isteminden Azure kaynaklarınızı hello Azure CLI toomanage kullanabilirsiniz. toocreate hello Azure CLI kullanarak VNet hello adımları izleyin.

1. Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../articles/cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.
2. Merhaba çalıştırmak **azure ağ vnet oluşturma** komut toocreate VNet ve alt ağ, aşağıda gösterildiği gibi. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    Beklenen çıktı:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **--vnet**. Merhaba VNet toobe oluşturulan adı. Bizim senaryomuz için bu *TestVNet* ’tir.
   * **-e (veya--adres alanı)**. VNet adres alanı. Bizim senaryomuz için *192.168.0.0*
   * **-i (veya - CIDR)**. Ağ maskesi CIDR biçiminde. Bizim senaryomuz için *16*.
   * **-n (veya--alt ağ adı**). Merhaba ilk alt ağ adı. Bizim senaryomuz için bu *FrontEnd* ’dir.
   * **-p (veya--alt başlangıç IP'sini)**. Alt ağ veya alt ağ adres alanı için başlangıç IP adresi. Bizim senaryomuz için *192.168.1.0*.
   * **-r (veya--alt ağ CIDR)**. Alt ağ için CIDR biçiminde ağ maskesi. Bizim senaryomuz için *24*.
   * **-l (veya --location)**. Merhaba Vnet'in oluşturulacağı azure bölgesi. Bizim senaryomuz için *Orta ABD*.
3. Merhaba çalıştırmak **azure ağ sanal alt ağ oluşturmak** komutu toocreate aşağıda gösterildiği gibi bir alt ağ. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    Yukarıdaki hello komut için beklenen hello çıktı şöyledir:
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t (veya--vnet-ad**. Merhaba hello alt oluşturulacağı Vnet'in adı. Bizim senaryomuz için bu *TestVNet* ’tir.
   * **-n (veya --name)**. Merhaba yeni alt ağ adı. Bizim senaryomuz için *arka uç*.
   * **-a (veya--adres-önek)**. Alt ağ CIDR bloğu. Dört bizim senaryomuz *192.168.2.0/24*.
4. Merhaba çalıştırmak **azure ağ vnet show** aşağıda gösterildiği gibi tooview hello hello yeni vnet'in özelliklerini komutu.
   
            azure network vnet show
   
    Yukarıdaki hello komut için beklenen hello çıktı şöyledir:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

