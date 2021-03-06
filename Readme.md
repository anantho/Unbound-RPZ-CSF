# Debian 10 Buster - Unbound Filter using https://energized.pro/

# install unbound DNS
> <p>apt install unbound python-unbound ca-certificates dnsutils

# create zones directory
> <p>mkdir -p /etc/unbound/zones
  
# download/copy paste and change permission script
> <p>wget https://raw.githubusercontent.com/anantho/Unbound-RPZ-CSF/master/usr/local/bin/ads_block.sh -O /usr/local/bin/ads_block.sh
> <p>wget https://raw.githubusercontent.com/anantho/Unbound-RPZ-CSF/master/usr/local/bin/porn_block.sh -O /usr/local/bin/porn_block.sh
> <p>wget https://raw.githubusercontent.com/anantho/Unbound-RPZ-CSF/master/usr/local/bin/update_named.sh -O /usr/local/bin/update_named.sh
> <p>chmod +x /usr/local/bin/ads_block.sh
> <p>chmod +x /usr/local/bin/porn_block.sh
> <p>chmod +x /usr/local/bin/update_named.sh

# crontab schedule
> <p>@monthly /usr/local/bin/update_named.sh #update root.hints</b>
> <p>@weekly /usr/local/bin/ads-block.sh #update ads & malware rpz blocking list
> <p>@weekly /usr/local/bin/porn-block.sh #update porn rpz blocking list

# Installing IPTables-persistent and IPSet-persistent
> <p>apt install iptables-persistent ipset-persistent curl

# Move to IPTables-Legacy
> <p>update-alternatives --set iptables /usr/sbin/iptables-legacy 
> <p>update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy 

# Download CSF Firewall
> <p>cd /opt/ 
> <p>wget http://download.configserver.com/csf.tgz 
> <p>tar xzf csf.tgz 

# Installing CSF
> <p>cd /opt/csf 
> <p>sh install.sh 

# Test CSF fuction
> <p>perl /usr/local/csf/bin/csftest.pl

# Run Service
> <p>systemctl restart unbound
> <p>systemctl enable csf
> <p>systemctl enable lfd
> <p>systemctl restart csf
> <p>systemctl restart lfd

# NOTE
<p>don't forget to put whitelist IP Address at /etc/csf/csf.ignore
