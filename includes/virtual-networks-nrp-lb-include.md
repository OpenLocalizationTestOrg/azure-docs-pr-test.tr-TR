## <a name="load-balancer"></a><span data-ttu-id="304b1-101">Yük Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="304b1-101">Load Balancer</span></span>
<span data-ttu-id="304b1-102">Bir yük dengeleyici uygulamalarınızı ölçeklendirme istediğinizde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="304b1-102">A load balancer is used when you want to scale your applications.</span></span> <span data-ttu-id="304b1-103">Tipik dağıtım senaryoları, birden çok VM örnekleri üzerinde çalışan uygulamalar içerir.</span><span class="sxs-lookup"><span data-stu-id="304b1-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="304b1-104">VM örnekleri, ağ trafiğini çeşitli örneklerine dağıtmak için yardımcı bir yük dengeleyici tarafından fronted.</span><span class="sxs-lookup"><span data-stu-id="304b1-104">The VM instances are fronted by a load balancer that helps to distribute network traffic to the various instances.</span></span> 

![NIC kişinin tek bir VM'de](./media/resource-groups-networking/figure8.png)

| <span data-ttu-id="304b1-106">Özellik</span><span class="sxs-lookup"><span data-stu-id="304b1-106">Property</span></span> | <span data-ttu-id="304b1-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="304b1-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="304b1-108">*Frontendıpconfigurations'a*</span><span class="sxs-lookup"><span data-stu-id="304b1-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="304b1-109">bir yük dengeleyici, aksi halde sanal IP (VIP) bilinen bir veya daha fazla ön uç IP adresi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="304b1-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="304b1-110">Bu IP adreslerine trafiği için giriş olarak hizmet ve genel IP veya özel IP olabilir.</span><span class="sxs-lookup"><span data-stu-id="304b1-110">These IP addresses serve as ingress for the traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="304b1-111">*Backendaddresspool*</span><span class="sxs-lookup"><span data-stu-id="304b1-111">*backendAddressPools*</span></span> |<span data-ttu-id="304b1-112">VM yük dağıtılacak NIC ile ilişkili IP adreslerini bunlar</span><span class="sxs-lookup"><span data-stu-id="304b1-112">these are IP addresses associated with the VM NICs to which load will be distributed</span></span> |
| <span data-ttu-id="304b1-113">*loadBalancingRules*</span><span class="sxs-lookup"><span data-stu-id="304b1-113">*loadBalancingRules*</span></span> |<span data-ttu-id="304b1-114">bir kural özelliği, belirtilen ön uç IP ve bağlantı noktası bileşimi için bir arka uç IP adresleri kümesini ve bağlantı noktası bileşimi eşler.</span><span class="sxs-lookup"><span data-stu-id="304b1-114">a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="304b1-115">Tek bir tanım yük dengeleyici kaynak birden çok Yük Dengeleme kuralları tanımlayabilirsiniz, her kural yalnızca bir ön bileşimini yansıtma IP ve bağlantı noktası bitiş ve bitiş IP ve sanal makinelerle ilişkili bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="304b1-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="304b1-116">Arka uç havuzundaki birçok sanal makineler için ön uç havuzundaki bir bağlantı noktası kuralıdır</span><span class="sxs-lookup"><span data-stu-id="304b1-116">The rule is one port in the front end pool to many virtual machines in the back end pool</span></span> |
| <span data-ttu-id="304b1-117">*Yoklamaları*</span><span class="sxs-lookup"><span data-stu-id="304b1-117">*Probes*</span></span> |<span data-ttu-id="304b1-118">araştırmalar VM örnekleri durumunu izlemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="304b1-118">probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="304b1-119">Bir sistem durumu araştırması başarısız olursa, sanal makine örneğini döndürme dışında otomatik olarak gerçekleştirilecek</span><span class="sxs-lookup"><span data-stu-id="304b1-119">If a health probe fails, the virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="304b1-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="304b1-120">*inboundNatRules*</span></span> |<span data-ttu-id="304b1-121">NAT kuralları önde gelen trafiği tanımlama IP sonlandırmak ve belirli bir sanal makine örneği için arka uç IP dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="304b1-121">NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP to a specific virtual machine instance.</span></span> <span data-ttu-id="304b1-122">NAT kuralı arka uç havuzundaki bir sanal makine için ön uç havuzundaki bir bağlantı noktasıdır</span><span class="sxs-lookup"><span data-stu-id="304b1-122">NAT rule is one port in the front end pool to one virtual machine in the back end pool</span></span> |

<span data-ttu-id="304b1-123">Yük Dengeleyici şablonu Json biçiminde örneği:</span><span class="sxs-lookup"><span data-stu-id="304b1-123">Example of load balancer template in Json format:</span></span>

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
            "description": "Location to deploy"
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

### <a name="additional-resources"></a><span data-ttu-id="304b1-124">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="304b1-124">Additional resources</span></span>
<span data-ttu-id="304b1-125">Okuma [yük dengeleyici REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="304b1-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>

