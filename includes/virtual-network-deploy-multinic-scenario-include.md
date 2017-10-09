## <a name="scenario"></a>Senaryo
Bu belge, birden çok NIC Vm'lerde belirli bir senaryoda kullanan bir dağıtım size yol gösterecek. Bu senaryoda, Azure üzerinde barındırılan bir iki katmanlı Iaas iş yükü vardır. Her katman kendi alt ağda bir sanal ağ (VNet) dağıtılır. bir yük dengeleyici için yüksek kullanılabilirlik kümesi içinde bir arada gruplandırılmış birkaç web sunucuları, Hello ön uç katmanından oluşur. birkaç veritabanı sunucularının Hello arka uç katmanından oluşur. Bu veritabanı sunucuları iki NIC içeren her bir veritabanı erişimi için dağıtılmış, diğer yönetim için hello. Hello senaryosu hello dağıtımında hangi trafiğe tooeach alt ağ ve NIC izin ağ güvenlik grupları (Nsg'ler) toocontrol de içerir. Aşağıdaki Hello şekilde bu senaryonun hello temel mimari gösterilmektedir.  

![MultiNIC senaryosu](./media/virtual-network-deploy-multinic-scenario-include/Figure1.png)

