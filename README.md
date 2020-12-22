# french-wikipedia-word-list

Pour les besoins d'un projet, il me fallait rapidement une liste de mots français la plus complète possible. J'ai récupéré un dump de wikipedia, retiré les  caractères supperflus sans modifier le codage utilisé, puis trié les mots.
Vous trouverez ici le fichier résultant (compressé).

Voici la liste de commande utilisée :

wget https://dumps.wikimedia.org/frwiki/latest/frwiki-latest-pages-articles-multistream.xml.bz2

(environ 5Go)

bzcat frwiki-latest-pages-articles-multistream.xml.bz2 | tr "\040\041\042\043\044\045\046\047\050\051\052\053\054\056\057\060\061\062\063\064\065\066\067\070\071\072\073\074\075\076\077\100\133\134\135\136\137\140\173\174\175\176" "\n" > toto

(cette commande dure environ 10mn, et le fichier toto fait environ 21Go)

cat toto | tr -s "\n" | sort | uniq > wikipedia.fr.txt

(cette commande dure environ 1h30, et le fichier wikipedia.fr.txt fait 311Mo)

wc -l wikipedia.fr.txt # la commande indique que le fichier fait 23 260 223 lignes

Avec la commande head, je cherche les premières lignes intéressantes du fichier, puis je supprime les N lignes précédentes
head -n 10500 wikipedia.fr.txt # 
tail -n+10500 wikipedia.fr.txt > toto

Même chose pour la fin du fichier :
tail -n+22481000 toto | more # pour trouver l'endroit où les choses se gâtent
head -n+22481000 toto > wikipedia.fr.txt

rm toto

Notes : Pour information, voici la table des codes ASCII (en octal) utilisée pour générer le premier fichier toto

Décimal Octal Hex Binaire Caractère

------- ----- --- -------- ------

032 040 20 00100000 SP (Space)

033 041 21 00100001 ! (exclamation mark)

034 042 22 00100010 " (double quote)

035 043 23 00100011 # (number sign)

036 044 24 00100100 $ (dollar sign)

037 045 25 00100101 % (percent)

038 046 26 00100110 & (ampersand)

039 047 27 00100111 ' (single quote)

040 050 28 00101000 ( (left opening parenthesis)

041 051 29 00101001 ) (right closing parenthesis)

042 052 2A 00101010 * (asterisk)

043 053 2B 00101011 + (plus)

044 054 2C 00101100 , (comma)



046 056 2E 00101110 . (dot)

047 057 2F 00101111 / (forward slash)

048 060 30 00110000 0

049 061 31 00110001 1

050 062 32 00110010 2

051 063 33 00110011 3

052 064 34 00110100 4

053 065 35 00110101 5

054 066 36 00110110 6

055 067 37 00110111 7

056 070 38 00111000 8

057 071 39 00111001 9

058 072 3A 00111010 : (colon)

059 073 3B 00111011 ; (semi-colon)

060 074 3C 00111100 < (less than sign)

061 075 3D 00111101 = (equal sign)

062 076 3E 00111110 > (greater than sign)

063 077 3F 00111111 ? (question mark)

064 100 40 01000000 @ (AT symbol)



091 133 5B 01011011 [ (left opening bracket)

092 134 5C 01011100 \ (back slash)

093 135 5D 01011101 ] (right closing bracket)

094 136 5E 01011110 ^ (caret cirumflex)

095 137 5F 01011111 _ (underscore)

096 140 60 01100000 `



123 173 7B 01111011 { (left opening brace)

124 174 7C 01111100 | (vertical bar)

125 175 7D 01111101 } (right closing brace)

126 176 7E 01111110 ~ (tilde)









