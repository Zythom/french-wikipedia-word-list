# french-wikipedia-word-list

Pour les besoins d'un projet, il me fallait rapidement une liste de mots français la plus complète possible. J'ai récupéré un dump de wikipedia, retiré les  caractères supperflus sans modifier le codage utilisé, puis trié les mots.
Vous trouverez ici le fichier résultant (compressé).

Voici la liste de commande utilisée :

wget https://dumps.wikimedia.org/frwiki/latest/frwiki-latest-pages-articles-multistream.xml.bz2
(environ 5Go)

bzcat frwiki-latest-pages-articles-multistream.xml.bz2 | tr "\040\041\042\043\044\045\046\047\050\051\052\053\054\056\057\060\061\062\063\064\065\066\067\070\071\072\073\074\075\076\077\100\133\134\135\136\137\140\173\174\175\176" "\n" > toto
(cette commande dure environ 10mn, et le fichier toto fait environ 21Go)

cat toto | tr -s "\n" | sort | uniq > wikipedia.fr.txt
(cette commande dure environ 1h30)

rm toto



