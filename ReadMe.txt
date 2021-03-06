＜お知らせ＞
Revision 2 のブラウザ・セキュリティ強化による不具合はRevision 3 にて解消しました。(Nov 15th 2019) 
過去版を使っていた場合には、SSL証明書キャッシュを削除する必要があります。管理画面のsystemから削除できます。

＜動作上の注意＞
このシステムは、下記の通りにインストールすればSWGとしては動作しますが、クライアント側でも作業が必要です。
{install directory}/config/ssl_cert.crt をブラウザの信頼できる認証局に登録してください。そうでないとブラウザで証明書エラーで拒否されます。
また、ブラウザのキャッシュ類がが残っていると、同一ドメインの本物の証明書と、SWGが発行する代理証明書が混在してしまうので、ブラウザキャッシュは必ずクリアして下さい。

また、今版ではSSL証明書の期限を2年としました。本来であれば、内部で発行したSSL証明書の期限が切れた、再発行する処理を実装する必要があるのですが、現在はこれを実装しておりません。　次回のリリースの際に、これらの対応を実施する予定です。　また、発行した証明書はブラウザの表示機能からも参照できます。

本システムは、openldapを使用しますので、Linuxマシンには openldapのインストールapt | yum 等で実施してから実行して下さい。


---------------------------------------------------
Takayuki.Uchida Japan (contact@u-software.co.jp)

This system has three challenges still. 
First, we don't have URL category database. this system can't be SWG without URL category database.
Next, we need testing and field verification. but we don't have enough resources.
Finally, this system has below functions (1)-(9). but it's not enough as next generation gateway system. 
so I'm finding new function that bring new value.

So that I need collaborators to develop together and coordinators to deploy around the world as New value gateway.
Please contact me!

		Skipper 
---------------------------------------------------
+ environment to deverlop
  I'm using "Visual Studio Express 2013 for Windows Desktop" to deverlop.
  If you can collaborate, you need same environments.

+ please ask me(contact@u-software.co.jp) about zip password.
    [attention please!]  I will give you special password,    !skipper123#     Please try this! 

<For Linux> 
*) we need [openldap] pkg when installing this system!
1. Install (Linux centos7)
  rpm -ihv skipper-swg-0.99-R03.x86_64.rpm   (uninstall: rpm -e ...,  list: rpm -qa | grep skipper)
      install to /usr/local/skipper/...
  systemctl start skipper | service skipper start
    - log: /usr/local/skipper/log/
    - default
       proxy port : 0.0.0.0/8080
       do [ssl intercept] all web-request.
  or
1. Install (Linux Ubuntu server)
   dpkg -i skipper-swg_0.99.3_amd64.deb  (unilstall: dpkg --purge ...,  list: dpkg --list | grep skipper)
      install to /usr/local/skipper/...
   service skipper start
2. You should get license-key from mail: skipper.worldchallege@gmail.com.
    you check GUI: Maintenance/Version and get [bliid /dev/sda1] and send get-value to mail.
      GUI: http://{install machine address}:9091   user[root] passwd[root]
    then I reply productId. you set this value.
    if you don't do this, proxy stop 30min after starting. but you can restart then you can use for 30min again.
    
<For Windows>    
1. Install WindowsServer2012R2 or more
      installer click only
      - install to service.  if you control skipper, you operate with [service].
      - install directory
           C:¥Program Files¥skipper1
     - default
       proxy port : 0.0.0.0/8080
       do [ssl intercept] all web-request.  
2. You should get license-key from mail: skipper.worldchallege@gmail.com.
   you check GUI: Maintenance/Version and get [ControlPanel - System - ProductID] and send get-value to mail.
       GUI: http://{install machine address}:9091    user[root] passwd[root]
   then I reply productId. you set this value.
   if you dont do this, proxy stop 30min after starting. but you can restart then you can use for 30min again.
   
--
Skipper is Valued-Secure Web Gateway and has specific any function below.

1) Supported HTTP/2 intercept(decode) and WebSocket, of couse HTTP/1, FTP.
2) To enbbed User Library is possible. 
3) Filterling
  - Now Skipper dont have URL-Filtering DB, But Skipper can filter WebRequest by ACL that Client set,
     Filter Target:
      URL/Host/HttpHeader/Query/SrcIp/Port/DstIp/Port/DstCountry/Protocol/…
      [**New R02] As new filter condition, OwnIPPort and SourceCountry
  - Skipper can filter WebRequest by [Snort] Rules and Reputation.
     as forward-proxy: upstream-direction only(home_net->external_net),  as reverse-proxy: upstream-direction only(external_net->home_net)
  * When blocking, this system doesnot display blocking-page, only disconnecting.
4) Multiple Authentiations(LDAP/NTLM/Private) 
5) Detailed Logging for SIEM.
6) Cache for static contents.
7) Rich Setting GUI.
8) Multi-environment as Windows, Linux.
9) [**New R02] Preverse Proxy function!

Now Skipper has any issue below.
- Skipper doesnt have URL-FilteringDB including Black/WhiteList and distribute such DB.
  ***** please provide these or make these together with me!   ask me! *******
- Skipper should have setting datas for reverse-proxy at connecting to CDN. for example http-header for client ip.

Possibility
- To enbbed User Library is possible. so that we can develop the Gateway Solution.
