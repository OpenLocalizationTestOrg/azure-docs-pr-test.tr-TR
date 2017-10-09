### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>Özel IPsec/IKE ilkesi tüm Azure VPN Gateway SKU’larında desteklenir mi?
Özel IPsec/IKE ilkesi, Azure **VpnGw1, VpnGw2, VpnGw3, Standard** ve **HighPerformance** VPN ağ geçitlerinde desteklenir. **Temel** SKU DESTEKLENMEZ.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>Bir bağlantıda kaç tane ilke belirtebilirim?
Belirli bir bağlantı için yalnızca ***bir*** ilke birleşimi belirtebilirsiniz.

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>Bir bağlantıda kısmi bir ilke belirtebilir miyim? (örneğin, IPsec olmadan yalnızca IKE algoritmaları)
Hayır, hem IKE (Ana Mod) hem de IPsec (Hızlı Mod) için tüm algoritmaları ve parametreleri belirtmeniz gerekir. Kısmi ilke belirtimine izin verilmez.

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>Merhaba algoritmaları ve anahtar gücü hello özel ilke desteklenen nelerdir?
desteklenen hello şifreleme algoritmaları ve anahtar gücü yapılandırılabilir hello müşteriler Hello tabloda listelenmiştir. Her alan için bir seçeneği belirlemeniz gerekir.

| **IPsec/IKEv2**  | **Seçenekler**                                                                   |
| ---              | ---                                                                           |
| IKEv2 Şifrelemesi | AES256, AES192, AES128, DES3, DES                                             |
| IKEv2 Bütünlüğü  | SHA384, SHA256, SHA1, MD5                                                     |
| DH Grubu         | DHGroup24, ECP384, ECP256, DHGroup14 (DHGroup2048), DHGroup2, DHGroup1, Hiçbiri |
| IPsec Şifrelemesi | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None      |
| IPsec Bütünlüğü  | GCMAES256, GCMAES192, GCMAES128, SHA256, SHA1, MD5                            |
| PFS Grubu        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, Hiçbiri                              |
| QM SA Yaşam Süresi   | Saniye (tamsayı; **en az 300**/varsayılan 27000 saniye)<br>Kilobayt (tamsayı; **en az 1024**/varsayılan 102400000 kilobayt)           |
| Trafik Seçicisi | UsePolicyBasedTrafficSelectors ($True/$False; varsayılan $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048 olan hello aynı Diffie-Hellman grubu olarak **14** IKE ve IPSec PFS. Lütfen bakın [Diffie-Hellman grupları](#DH) Merhaba eşlemeleri tamamlayın.
> 2. GCMAES algoritmalar için belirtmelisiniz IPSec şifreleme ve bütünlük için aynı GCMAES algoritması ve anahtar uzunluğu hello.
> 3. Ikev2 ana mod SA ömrü hello Azure VPN ağ geçitlerinde 28.800 saniyedir adresindeki sabit
> 4. QM SA Yaşam Süreleri isteğe bağlı parametrelerdir. Hiçbiri belirtilmemişse, varsayılan 27.000 saniye (7,5 saat) ve 102400000 kilobayt (102 GB) değerleri kullanılır.
> 5. UsePolicyBasedTrafficSelector hello bağlantıda bir seçenek parametresidir. Lütfen hello sonraki SSS görmek için "UsePolicyBasedTrafficSelectors" öğesi

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>Her şeyi hello Azure VPN ağ geçidi İlkesi my şirket içi VPN cihaz yapılandırmalarını arasındaki toomatch gerekiyor mu?
Şirket içi VPN cihazınızın yapılandırması eşleşmiyor veya algoritmaları aşağıdaki hello içeren ve Azure IPSec/IKE İlkesi belirttiğiniz parametreleri hello:

* IKE şifreleme algoritması
* IKE bütünlük algoritması
* DH Grubu
* IPsec şifreleme algoritması
* IPsec bütünlük algoritması
* PFS Grubu
* Trafik Seçicisi (*)

Merhaba SA yaşam süreleri yalnızca yerel belirtimleri, toomatch gerekmez.

Etkinleştirirseniz, **UsePolicyBasedTrafficSelectors**, VPN cihazınız vardır, şirket içi ağ (yerel ağ geçidi) önekleri denetleyicisinden hello tüm bileşimleri ile tanımlanmış trafiğini Seçici eşleşen hello tooensure gerekir Any herhangi yerine Azure sanal ağı önekleri. Örneğin, 10.1.0.0/16 ve 10.2.0.0/16, şirket içi ağ ön ekleri ve 192.168.0.0/16 ve 172.16.0.0/16, sanal ağ ön ekleri, trafik Seçici aşağıdaki toospecify hello gerekir:
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

Çok başvuran[birden çok şirket içi ilke tabanlı VPN aygıtlarını bağlamak](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) konusunda daha fazla ayrıntı için toouse bu seçeneği.

### <a name ="DH"></a>Hangi Diffie-Hellman Grupları desteklenir?
Merhaba tabloda IKE (DHGroup) ve IPSec (PFSGroup) için desteklenen hello Diffie-Hellman grupları listelenir:

| **Diffie-Hellman Grubu**  | **DHGroup**              | **PFSGroup** | **Anahtar uzunluğu** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | 768 bit MODP   |
| 2                         | DHGroup2                 | PFS2         | 1024 bit MODP  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | 2048 bit MODP  |
| 19                        | ECP256                   | ECP256       | 256 bit ECP    |
| 20                        | ECP384                   | ECP284       | 384 bit ECP    |
| 24                        | DHGroup24                | PFS24        | 2048 bit MODP  |
|                           |                          |              |                |

Çok başvuran[RFC3526](https://tools.ietf.org/html/rfc3526) ve [RFC5114](https://tools.ietf.org/html/rfc5114) daha fazla ayrıntı için.

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>Merhaba özel ilke hello varsayılan IPSec/IKE İlkesi kümeleri Azure VPN ağ geçitleri için yerini almaz?
Özel bir ilke bir bağlantıda belirlendikten sonra Evet, Azure VPN ağ geçidi yalnızca hello İlkesi hello bağlantıda, hem de IKE başlatıcı ve IKE Yanıtlayıcı olarak kullanır.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>Özel bir IPSec/IKE ilke kaldırırsanız, hello bağlantı korumasız hale gelir mi?
Hayır, hello bağlantı hala IPSec/IKE tarafından korunur. Öğesinden bir bağlantı hello özel ilke kaldırdıktan sonra hello Azure VPN ağ geçidi arka toohello döner [IPSec/IKE teklifleri varsayılan listesini](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) ve hello IKE el sıkışma şirket içi VPN Cihazınızı yeniden ile yeniden başlatın.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>Bir IPsec/IKE ilkesinin eklenmesi veya güncelleştirilmesi, VPN bağlantımı kesintiye uğratır mı?
Evet, Hello Azure VPN ağ geçidi hello var olan bağlantıyı kesmeden ve hello IKE el sıkışma toore yeniden başlat küçük kesintisi (birkaç saniye) neden-hello IPSec tüneli hello yeni şifreleme algoritmaları ve parametreleri. Lütfen şirket içi VPN aygıtınızın ayrıca hello eşleşen algoritmaları ve anahtar gücü toominimize hello kesintisi ile yapılandırıldığından emin olun.

### <a name="can-i-use-different-policies-on-different-connections"></a>Farklı bağlantılarda farklı ilkeler kullanabilir miyim?
Evet. Özel ilkeler, bağlantı başına bir ilke temelinde uygulanır. Farklı bağlantılarda farklı IPsec/IKE ilkeleri oluşturabilir ve uygulayabilirsiniz. Ayrıca, bir alt kümesini bağlantıları özel ilkeler tooapply tercih edebilirsiniz. olanları kalan hello hello Azure varsayılan IPSec/IKE İlkesi kümeleri kullanır.

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>Merhaba özel ilke de VNet-VNet bağlantısı üzerinde kullanabilir miyim?
Evet, hem IPsec şirket içi ve dışı karışık bağlantılarda hem de Vnet-Vnet bağlantılarında özel ilke uygulayabilirsiniz.

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>Toospecify gerekiyor mu hello her iki VNet-VNet bağlantı kaynaklar aynı ilke?
Evet. VNet-VNet tüneli, her iki yön için birer tane olmak üzere Azure’daki iki bağlantı kaynağından oluşur. Her iki bağlantı kaynaklarına sahip tooensure ihtiyacınız hello aynı ilke othereise hello VNet-VNet bağlantısı olmayan kurar.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>Özel IPsec/IKE ilkesi ExpressRoute bağlantısında çalışır mı?
Hayır. IPSec/IKE ilkesi yalnızca S2S VPN ve VNet-VNet bağlantıları hello Azure VPN ağ geçitleri aracılığıyla üzerinde çalışır.
