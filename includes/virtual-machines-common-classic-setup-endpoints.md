
Her bitiş noktasının bir *genel bağlantı noktası* ve *özel bağlantı noktası*:

* Merhaba genel bağlantı noktası gelen trafiği toohello sanal makineden hello Internet hello Azure yük dengeleyici toolisten tarafından kullanılır.
* Merhaba özel bağlantı noktası tarafından hello sanal makine toolisten gelen trafik, genellikle hedefleyen tooan uygulama veya hello sanal makinede çalışan hizmet için kullanılır.

IP protokolü için varsayılan değerleri hello ve uç noktaları hello Azure portal ile oluşturduğunuzda, TCP veya UDP bağlantı noktaları için iyi bilinen ağ protokolleri sağlanır. Özel uç noktaları için toospecify hello doğru IP Protokolü (TCP veya UDP) ve hello ortak ve özel bağlantı noktaları gerekir. birden çok sanal makine arasında rastgele toodistribute gelen trafik, birden çok uç noktaları oluşan bir yük dengeli kümesi toocreate gerekir.

Bir uç nokta oluşturduktan sonra izin veren veya toohello hello uç noktasının kaynak IP adresine göre genel bağlantı noktası hello gelen trafiği engelleyen bir erişim denetim listesi (ACL) toodefine kurallarını kullanabilirsiniz. Ancak, Hello sanal makine bir Azure sanal ağında ise, ağ güvenlik grupları yerine kullanmanız gerekir. Ayrıntılar için bkz [ağ güvenlik grupları hakkında](../articles/virtual-network/virtual-networks-nsg.md).

> [!NOTE]
> Azure sanal makineleri için güvenlik duvarı yapılandırması, Azure otomatik olarak ayarlayan uzak bağlantı uç ile ilişkili bağlantı noktaları için otomatik olarak yapılır. Diğer uç için belirtilen bağlantı noktaları için herhangi bir yapılandırma toohello Güvenlik Duvarı'nı hello sanal makinenin otomatik olarak yapılır. Merhaba sanal makine için bir uç nokta oluşturduğunuzda, gerekir güvenlik duvarı hello sanal makinenin hello tooensure hello trafiği hello protokolü ve özel bağlantı noktası karşılık gelen toohello uç nokta yapılandırması için de sağlar. tooconfigure güvenlik duvarı Merhaba, hello belgelerine veya hello sanal makinede çalışan hello işletim sistemi için çevrimiçi yardıma bakın.
>
>

## <a name="create-an-endpoint"></a>Uç nokta oluşturma
1. Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **sanal makineleri**ve ardından tooconfigure istediğiniz hello sanal makine hello adına tıklayın.
3. Tıklatın **uç noktaları** hello içinde **ayarları** grubu. Merhaba **uç noktaları** sayfası hello geçerli uç noktalar tüm hello sanal makine için listeler. (Bu örnek bir Windows VM'dir. Bir Linux VM varsayılan bir uç nokta için SSH gösterir.)

   <!-- ![Endpoints](./media/virtual-machines-common-classic-setup-endpoints/endpointswindows.png) -->
   ![Uç Noktalar](./media/virtual-machines-common-classic-setup-endpoints/endpointsblade.png)

4. Merhaba komut çubuğunda hello uç noktası girişleri yukarıda tıklayın **Ekle**.
5. Merhaba üzerinde **uç nokta ekleme** sayfasında, içindeki hello uç nokta için bir ad yazın **adı**.
6. İçinde **Protokolü**, ya da seçin **TCP** veya **UDP**.
7. İçinde **genel bağlantı noktası**, hello Internet hello giden trafiği için hello bağlantı noktası numarasını yazın. İçinde **özel bağlantı noktası**, sanal makine üzerinde hangi hello dinlerken hello bağlantı noktası numarasını yazın. Bu bağlantı noktası numaralarını farklı olabilir. Bu hello olun hello sanal makine üzerinde güvenlik duvarı yapılandırılmış tooallow hello trafiği karşılık gelen toohello protokolünde (6. adım) ve özel bağlantı noktası açıldı.
10. **Tamam**’a tıklayın.

Merhaba yeni uç noktası üzerinde hello listelenir **uç noktaları** sayfası.

![Uç nokta oluşturma başarılı](./media/virtual-machines-common-classic-setup-endpoints/endpointcreated.png)

## <a name="manage-hello-acl-on-an-endpoint"></a>Bir uç noktasındaki ACL Hello yönetme
trafik gönderebilen bilgisayar toodefine hello kümesi, kaynak IP adresine göre trafiği bir uç noktasındaki ACL hello kısıtlayabilirsiniz. Bu adımları tooadd izleyin, değiştirme veya bir uç nokta ACL'sini kaldırın.

> [!NOTE]
> Hello uç nokta yük dengeli kümesinin bir parçası ise, bir uç noktasındaki ACL olan toohello uygulanan tooall uç noktaları hello kümesinde değişiklik.
>
>

Merhaba sanal makine bir Azure sanal ağında ise, ağ güvenlik grupları, ACL yerine öneririz. Ayrıntılar için bkz [ağ güvenlik grupları hakkında](../articles/virtual-network/virtual-networks-nsg.md).

1. Zaten yapmadıysanız, toohello Azure portalında oturum açın.
2. Tıklatın **sanal makineleri**ve ardından tooconfigure istediğiniz hello sanal makine hello adına tıklayın.
3. **Uç Noktalar**’a tıklayın. Merhaba listeden hello uygun uç nokta seçin. Merhaba ACL hello hello sayfa sonunda listelenmiştir.

   ![ACL ayrıntılarını belirtin](./media/virtual-machines-common-classic-setup-endpoints/aclpreentry.png)

4. Hello kullan satır tooadd, delete ya da Düzenle kuralları için bir ACL listesi ve bunların sırasını değiştirin. Merhaba **uzak alt** hello Azure yük dengeleyici kullanan toopermit hello veya kaynak IP adresine göre hello trafiği reddeden Internet giden trafiği için bir IP adresi aralığı bir değerdir. CIDR biçiminde adres öneki biçimi olarak da bilinen emin toospecify hello IP adres aralığı olabilir. Örnek `10.1.0.0/8`.

 ![Yeni ACL giriş](./media/virtual-machines-common-classic-setup-endpoints/newaclentry.png)


Kuralları tooallow yalnızca trafiğini hello Internet veya toodeny trafiği belirli, bilinen adres aralıklarından tooyour bilgisayarlarda karşılık gelen belirli bilgisayarlardan kullanabilirsiniz.

Merhaba kuralları hello ilk kural ile başlayıp hello son kuralla sırayla değerlendirilir. Bu kurallar en az kısıtlayıcı toomost kısıtlayıcı sıralanmalıdır anlamına gelir. Örnekler ve daha fazla bilgi için bkz: [bir ağ erişim denetimi listesi nedir](../articles/virtual-network/virtual-networks-acl.md).
