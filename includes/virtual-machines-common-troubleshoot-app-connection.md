Başlattığınızda veya bir Azure sanal makine (VM) üzerinde çalışan tooan bağlamak çeşitli nedenleri vardır. Nedenler çalışmıyor hello uygulamayı ekleme veya hello beklenen bağlantı noktalarında dinleme hello engellendi veya doğru biçimde trafiği toohello uygulama geçirme kuralları ağ dinleme bağlantı noktası. Bu makalede sistemli yaklaşım toofind ve doğru hello sorunu açıklanır.

Tooyour VM bağlantı sorunları yaşıyorsanız RDP veya SSH, kullanarak bkz hello Aşağıdaki makaleler önce:

* [Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine sorunlarını giderme](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* [Güvenli Kabuk (SSH) bağlantı tooa Linux tabanlı Azure sanal makine sorun giderme](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../articles/resource-manager-deployment-model.md). Bu makalede, her iki modeli kullanarak yer almaktadır, ancak Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure hello ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.

## <a name="quick-start-troubleshooting-steps"></a>Hızlı Başlangıç sorun giderme adımları
Tooan uygulama bağlantı sorunlarınız varsa, genel sorun giderme adımlarını izleyerek hello deneyin. Her adımdan sonra bağlanan tooyour uygulamayı yeniden deneyin:

* Merhaba sanal makineyi yeniden başlatın
* Merhaba uç noktası oluşturun / kuralları güvenlik duvarı / ağ güvenlik grubu (NSG) kuralları
  * [Resource Manager modeli - ağ güvenlik gruplarını yönetme](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [Klasik model - Cloud Services'ı Yönet uç noktaları](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* Farklı bir Azure sanal ağı gibi farklı bir konumdan bağlanma
* Merhaba sanal makineyi yeniden dağıtın
  * [Windows VM yeniden dağıtın](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [Linux VM yeniden dağıtın](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* Merhaba sanal makine oluşturun

Daha fazla bilgi için bkz: [sorun giderme uç noktası bağlantısı (RDP/SSH/HTTP, vb. hataları)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).

## <a name="detailed-troubleshooting-overview"></a>Ayrıntılı sorun giderme genel bakış
Bir Azure sanal makine üzerinde çalışan bir uygulama tootroubleshoot hello erişim dört temel konu vardır.

![sorun giderme uygulaması başlatılamıyor](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. Hello Azure sanal makine üzerinde çalışan hello uygulama.
   * Merhaba uygulamanın kendisinin düzgün çalışıyor mu?
2. Hello Azure sanal makine.
   * Merhaba VM kendisini doğru şekilde çalıştığını ve toorequests yanıt?
3. Azure ağı uç noktaları.
   * Hizmet uç noktaları hello Klasik dağıtım modelinde sanal makineler için bulut.
   * Ağ güvenlik grupları ve Resource Manager dağıtım modelinde sanal makineler için gelen NAT kuralları.
   * Kullanıcıların toohello VM/uygulama hello beklenen bağlantı noktalarında akışından trafiği?
4. Internet sınır cihazı.
   * Güvenlik duvarı kuralları yerinde doğru akan trafik engelliyor?

Merhaba uygulaması siteden siteye VPN veya ExpressRoute bağlantısı üzerinden erişmekte olan istemci bilgisayarlar için sorunlara neden olabilecek hello ana alanlar Merhaba uygulaması ve Azure sanal makinesi hello.

toodetermine hello kaynağını hello sorun, düzeltme ve aşağıdaki adımları izleyin.

## <a name="step-1-access-application-from-target-vm"></a>Adım 1: hedef VM uygulamaya erişim
Merhaba VM üzerinde çalıştığı hello uygun istemci programla tooaccess hello uygulamayı deneyin. Merhaba yerel ana bilgisayar adı, hello yerel IP adresi veya hello geri döngü adresine (127.0.0.1) kullanın.

![doğrudan hello VM ' uygulama Başlat](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

Örneğin, hello uygulama bir web sunucusu ise, hello VM üzerinde bir tarayıcı açın ve tooaccess hello VM üzerinde barındırılan bir web sayfasına deneyin.

Merhaba uygulaması erişebiliyorsa çok Git[2. adım](#step2).

Merhaba uygulaması erişemiyorsanız, ayarlar aşağıdaki hello doğrulayın:

* Merhaba uygulaması hello hedef sanal makinede çalışıyor.
* Merhaba uygulaması beklenen hello TCP ve UDP bağlantı noktalarını dinler.

Hem Windows hem de Linux tabanlı sanal makineleri hello kullan **netstat - a** tooshow hello etkin dinleme bağlantı noktalarını komutu. Uygulamanızı dinleniyor olması beklenen hello bağlantı noktaları için Hello çıktıyı inceleyin. Merhaba uygulamayı yeniden başlatın veya toouse beklenen hello bağlantı noktalarını gerektiği gibi yapılandırın ve tooaccess hello uygulamayı yerel olarak yeniden deneyin.

## <a id="step2"></a>2. adım: Hello başka bir VM'den uygulama erişim aynı sanal ağ
Farklı bir VM tooaccess hello uygulamadan deneyin ancak içinde aynı hello hello VM'in ana bilgisayar adı veya Azure tarafından atanan genel, özel veya sağlayıcı IP adresini kullanarak sanal ağ. Merhaba Klasik dağıtım modeli kullanılarak oluşturulan sanal makineler için hello bulut hizmeti hello genel IP adresi kullanmayın.

![farklı bir sanal makineden uygulama Başlat](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

Örneğin, bir web sayfasında farklı bir VM üzerinde bir tarayıcıdan try tooaccess Hello uygulama bir web sunucusu ise, aynı sanal ağ hello.

Merhaba uygulaması erişebiliyorsa çok Git[adım 3](#step3).

Merhaba uygulaması erişemiyorsanız, ayarlar aşağıdaki hello doğrulayın:

* Merhaba gelen istek ve yanıt giden trafiği Hello ana bilgisayar Güvenlik Duvarı'nı hello hedef VM izin verir.
* Yetkisiz erişim algılama veya ağ hello hedef VM üzerinde çalışan yazılımı izleme hello trafiğe izin verdiğinden.
* Bulut Hizmetleri uç noktaları veya ağ güvenlik grupları hello trafiğe izin:
  * [Klasik model - Cloud Services'ı Yönet uç noktaları](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [Resource Manager modeli - ağ güvenlik gruplarını yönetme](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* Merhaba yolunda, VM'deki arasında hello test VM ve yük dengeleyici veya güvenlik duvarı gibi VM çalıştıran ayrı bir bileşen hello trafiğe izin verdiğinden.

Merhaba güvenlik duvarı kuralları, uygulamanızın gelen ve giden trafik hariç tutmak isteyip bir Windows tabanlı sanal makineye Gelişmiş Güvenlik toodetermine ile Windows Güvenlik Duvarı'nı kullanın.

## <a id="step3"></a>3. adım: uygulama hello sanal ağ dışından erişim
Merhaba uygulamanın çalıştığı hello VM olarak hello sanal ağ dışındaki bir bilgisayardan tooaccess Merhaba uygulaması deneyin. Farklı bir ağ özgün istemci bilgisayarınız kullanın.

![Merhaba sanal ağ dışındaki bir bilgisayardan uygulama Başlat](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

Örneğin, Hello uygulama bir web sunucusu ise, tooaccess hello web sayfası hello sanal ağında olmayan bir bilgisayarda çalışan bir tarayıcıdan deneyin.

Merhaba uygulaması erişemiyorsanız, ayarlar aşağıdaki hello doğrulayın:

* VM'ler için hello Klasik dağıtım modeli kullanılarak oluşturulmuş:
  
  * Merhaba VM hello gelen trafiğe, özellikle hello Protokolü (TCP veya UDP) ve hello ortak ve özel bağlantı noktası numaralarını izin vermek için bu hello uç nokta yapılandırması doğrulayın.
  * Erişim denetim listelerini (ACL'ler) hello noktadaki hello Internet giden trafiği engellemediğini doğrulayın.
  * Daha fazla bilgi için bkz: [nasıl tooSet yukarı uç noktaları tooa sanal makine](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Merhaba Resource Manager dağıtım modeli kullanılarak oluşturulan VM'ler için:
  
  * Merhaba VM hello gelen trafiğe, özellikle hello Protokolü (TCP veya UDP) ve hello ortak ve özel bağlantı noktası numaralarını izin vermek için gelen NAT kuralı yapılandırmasını hello doğrulayın.
  * Ağ güvenlik grupları hello gelen istek ve yanıt giden trafiği izin emin olun.
  * Daha fazla bilgi için bkz. [Ağ Güvenlik Grubu (NSG) nedir?](../articles/virtual-network/virtual-networks-nsg.md)

Merhaba sanal makine ya da uç nokta yük dengeli bir küme üyesi ise:

* Hello araştırma Protokolü (TCP veya UDP) ve bağlantı noktası numarasının doğru olduğundan emin olun.
* Merhaba araştırma protokolü ve bağlantı noktası ise hello yük dengeli kümesi protokolü ve bağlantı noktası farklı:
  * Merhaba uygulaması hello araştırma Protokolü (TCP veya UDP) ve bağlantı noktası üzerinde dinleme yaptığını doğrulayın (kullanmak **netstat – a** VM üzerinde hello hedef).
  * Bu hello ana bilgisayar Güvenlik Duvarı'nı hello hedef VM hello gelen araştırma isteğinin ve giden araştırma yanıtı trafiği izin verdiğinden emin olun.

Merhaba uygulaması erişebiliyorsanız, Internet kenar Cihazınızı izin verdiğinden emin olmak:

* Merhaba giden uygulama isteği trafiği, istemci bilgisayar toohello Azure sanal makine.
* gelen uygulama yanıt hello Azure sanal makinesi trafiğinden hello.

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a>Merhaba uygulaması, IP doğrula toocheck hello ayarları kullan erişemiyorsanız adım 4. 

Daha fazla bilgi için bkz: [izlemeye genel bakış Azure ağ](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="additional-resources"></a>Ek kaynaklar
[Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine sorunlarını giderme](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[Güvenli Kabuk (SSH) bağlantı tooa Linux tabanlı Azure sanal makine sorunlarını giderme](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

