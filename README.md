SSTI wordlist is taken from: https://raw.githubusercontent.com/err0rr/SSTI/refs/heads/master/Wordlist (without fork, i wanted to store it in my repository)


## Creating wordpress wordlist

```
#!/bin/bash
> wp-plugins-top5000.txt
for page in $(seq 1 50); do
  curl -sg "https://api.wordpress.org/plugins/info/1.2/?action=query_plugins&request[browse]=popular&request[per_page]=100&request[page]=${page}" > /tmp/wp_page.json
  python3 -c "import json; [print(p['slug']) for p in json.load(open('/tmp/wp_page.json')).get('plugins',[])]" >> wp-plugins-top5000.txt
  echo "strona ${page}, razem: $(wc -l < wp-plugins-top5000.txt)"
  sleep 0.3
done
EOF
bash scrape.sh
```
