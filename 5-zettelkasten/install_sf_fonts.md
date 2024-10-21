```BASH title:fonts.sh
wget -P ~/.local/share/fonts https://github.com/sahibjotsaggu/San-Francisco-Pro-Fonts/archive/refs/heads/master.zip \
&& cd ~/.local/share/fonts \
&& unzip master.zip \
&& rm master.zip \
&& fc-cache -fv
```