### <a name="prepare-for-a-push-installation-on-a-linux-server"></a>Bir Linux sunucusu üzerinde göndererek yüklemeye hazırlanma

1. Merhaba Linux bilgisayarı ve hello işlem sunucusu arasında ağ bağlantısı olduğundan emin olun.
2. Bu hello işlem sunucusu tooaccess hello bilgisayar kullanabilir bir hesap oluşturun. Merhaba hesabı olmalıdır bir **kök** hello kaynak Linux sunucu üzerindeki kullanıcı. (Yalnızca hello göndermeli yüklemesi için ve güncelleştirmeleri için bu hesabı kullanın.)
3. Merhaba kaynak sunucu tüm ağ bağdaştırıcıları ile ilişkili hello yerel ana bilgisayar adı tooIP adresleri eşleyin girişlerine sahip Linux bu hello/etc/hosts dosyasını denetleyin.
4. Merhaba son openssh, openssh sunuculu ve openssl paketleri tooreplicate istediğiniz hello bilgisayara yükleyin.
5. Secure Shell’in (SSH) etkin olduğundan ve bağlantı noktası 22’de çalıştırıldığından emin olun.
6. SFTP alt sistemi ve parola kimlik doğrulaması hello sshd_config dosyasında etkinleştirin:
  1.  **Kök** kullanıcı olarak oturum açın.
  2.  İçinde dosya/etc/ssh hello/hello satır Bul sshd_config dosya başlıyorsa **PasswordAuthentication**.
  3.  Merhaba satırı açıklamadan çıkarın ve hello değeri çok değiştirin**Evet**.
  4.  İle başlayan Bul hello satır **alt sistemi** ve hello satırı açıklamadan çıkarın.

     ![Linux](./media/site-recovery-prepare-push-install-mob-svc-lin/mobility2.png)
  5. Merhaba yeniden **sshd** hizmet.

7. CSPSConfigtool içinde oluşturulan hello hesabını ekleyin.
    1.  Tooyour yapılandırma sunucusunda oturum açın.
    2.  **cspsconfigtool.exe** dosyasını açın. (Merhaba masaüstünde ve hello %ProgramData%\home\svsystems\bin klasöründeki bir kısayol olarak bulunur.)
    3.  Merhaba üzerinde **hesaplarını yönetme** sekmesini tıklatın, **hesabı Ekle**.
    4.  Oluşturduğunuz hello hesabı ekleyin. 
    5.  Bir bilgisayar için çoğaltma etkinleştirdiğinizde, kullandığınız hello kimlik bilgilerini girin.
