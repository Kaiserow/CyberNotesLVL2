NOT: DNS'in nasıl işlediğini anlamak için, https://github.com/Kaiserow/Bug-Bounty/blob/main/posts/01-%20DNS.md adresini kullanabilirsiniz. 

Bu kısımda sadece ilgili linkteki bilgilere ek olarak bazı noktalardan bahsedilecektir.

#  DNS Message Format

DNS, serverler arasındaki iletişmide bazı mesaj formatları (message format) kullanır. Bunkar şu şekildedir;

#### Question -> Name server için soru içerir. (Örneğin, www.google.com domain'inin IP adresi nedir? gibi)

#### Answer -> Resource Records (yani kaynaktan alınan A,AAAA gibi kayıtlar) ile sorular cevaplanır. (www.google.com domain adresinin IP adresi nedir? sorusuna verilen cevabın bir A kaydı olarak 216.58.212.4 içermesi gibi.)

#### Authority -> Bir domain için kimin yetkili olduğunu söyler. Örneğin, root server'ı, domain ile ilgili TLD serverlarının adreslerini recursive DNS serverına bildirirken Authority ksımına -> .com için TLD Server adresleri belirtilir.

#### Additional -> Ek bilgi içeren recordlar ile ilgilidir. Yukarıdaki örneğe göre, TLD serverlarının IP adreslerini içerebilir. (Authority kısmındaki adresler isim olarak belirtilirken bu kısımdakiler ise direk IP adreslerini verir.)

# DNS Hierarchy

Naming yapısı küçük, yönetilebilir bölgelere (zone) ayrılmıştır. Her DNS sunucusu belirli bir veritabanı dosyasını korur ve yalnızca tüm DNS yapısının o küçük kısmı için name-IP eşlemelerini yönetmekten sorumludur. Bir DNS sunucusu DNS bölgesinde olmayan bir ad çevirisi için bir istek aldığında, DNS sunucusu isteği çeviri için uygun bölgedeki başka bir DNS sunucusuna iletir. DNS ölçeklenebilirdir (scalable) çünkü hostname çözümlemesi birden fazla sunucuya yayılmıştır.

# The nslookup Command

nslookup komutu, işletim sistemlerinin sunmuş olduğu manuel olarak domain name sorgulama yöntemidir. Bu komut, name resolutionla ilgili sorunları ve name serverlarının düzgün çalışıp çalışmadıklarını tespit etmek için kullanılabilir. (Komut satırı üzerinden nslookup + domain name vererek test edebilirsiniz.)




