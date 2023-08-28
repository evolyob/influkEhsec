- [ ] 升級nmap資料庫
>nmap --script-updatedb 

- [ ] 漏洞掃描
>nmap -sV --script vuln <target>

- [ ] 是否有CSRF漏洞
>nmap -sV --script http-csrf <target>

- [ ] 是否有XSS漏洞
>nmap -sV --script http-xssed <target>

- [ ] 首頁haeders資訊
>nmap --script http-haeders <target>

- [ ] 主機獲取時間
>nmap --script http-date -p 443 

- [ ] 檢查可存在風險，感覺只是告訴我能用什麼方式。
>nmap --script http-methods -p 443 

- [ ] 目錄結構
>nmapnmap --script http-sitemap-generator -p 443 

- [ ] 443 port憑證
>nmap --script ssl-cert -p 443 <target>

- [ ] 443 port cipher
>nmap --script ssl-enum-ciphers -p 443 <target>

- [ ] 22 port使用的cipher
>nmap --script ssh2-enum-algos -p 22 <target>

- [ ] 發現文件
>nmap -sV --script http-enum <target>

- [ ] 路由追蹤
>nmap --traceroute -sP <target>
>tracepath -n <target> 

- [ ] 探測防火牆規則
>nmap --script firewalk --traceroute <target>
