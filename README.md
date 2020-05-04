# hyricsdic
Hyricsの単語の意味一覧を機械的に
# How?
```bash
cat (hyricsのデータ) | srings | grep -oP '[a-zA-Z]+' | tr A-Z a-z |
sort | uniq | ruby -ple'$_="#{$_.size} #{$_}"' | sort -V | awk '$1>2{print$2}' |
while read i;do echo $i $(curl -s "https://ejje.weblio.jp/content/${i}" |
grep 主な意味 | grep -oP '(?<=<td class="content-explanation ej">)[^<]+(?=/td>)')
sleep 0.1
done | awk 'NR>1{print$0}' > dic_mean
```
