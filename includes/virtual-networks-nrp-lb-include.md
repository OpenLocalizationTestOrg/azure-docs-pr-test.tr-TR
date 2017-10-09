## <a name="load-balancer"></a>Yük Dengeleyici
Bir yük dengeleyici, uygulamalarınızı tooscale istediğinizde kullanılır. Tipik dağıtım senaryoları, birden çok VM örnekleri üzerinde çalışan uygulamalar içerir. Merhaba VM örnekleri toodistribute ağ trafiği toohello çeşitli örnekler yardımcı olan bir yük dengeleyici tarafından fronted. 

![NIC kişinin tek bir VM'de](./media/resource-groups-networking/figure8.png)

| Özellik | Açıklama |
| --- | --- |
| *Frontendıpconfigurations'a* |bir yük dengeleyici, aksi halde sanal IP (VIP) bilinen bir veya daha fazla ön uç IP adresi içerebilir. Bu IP adreslerine hello trafiği için giriş olarak hizmet ve genel IP veya özel IP olabilir. |
| *Backendaddresspool* |VM NIC'ler toowhich yük dağıtılan hello ile ilişkili IP adreslerini bunlar |
| *loadBalancingRules* |bir kural özelliğine verilen ön uç IP eşler ve bağlantı noktası bileşimi tooa arka uç IP adresleri kümesini ve bağlantı noktası bileşimi. Tek bir tanım yük dengeleyici kaynak birden çok Yük Dengeleme kuralları tanımlayabilirsiniz, her kural yalnızca bir ön bileşimini yansıtma IP ve bağlantı noktası bitiş ve bitiş IP ve sanal makinelerle ilişkili bağlantı noktası. bir bağlantı noktası hello ön uç havuzu toomany sanal makinelerde hello arka uç havuzundaki Hello kuralıdır |
| *Yoklamaları* |araştırmalar VM örnekleri hello durumunu tookeep izlemeyi etkinleştirin. Bir sistem durumu araştırması başarısız olursa, hello sanal makine örneğini döndürme dışında otomatik olarak gerçekleştirilecek |
| *inboundNatRules* |NAT kuralları Hello tanımlama hello ön uç IP üzerinden giden trafiği gelen ve toohello arka uç IP tooa belirli bir sanal makine örneği dağıtılır. NAT kuralı hello ön uç havuzu tooone sanal makinede hello arka uç havuzundaki bir bağlantı noktasıdır |

Yük Dengeleyici şablonu Json biçiminde örneği:

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location toodeploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[parameters('location')]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[parameters('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[parameters('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a>Ek kaynaklar
Okuma [yük dengeleyici REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) daha fazla bilgi için.

