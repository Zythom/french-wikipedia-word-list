# french-wikipedia-word-list

Pour les besoins d'un projet, il me fallait rapidement une liste de mots français la plus complète possible, avec villes, départements, noms propres, etc. En suivant la méthode préconisée par l'IILaR (International Institute of La RACHE https://www.la-rache.com/), j'ai récupéré un dump du wikipedia français, retiré les  caractères superflus sans modifier le codage utilisé, puis trié les mots.

Afin d'éviter de surcharger inutilement les sites de Wikipédia, vous trouverez ici le fichier résultant (297Mo), à reconstituer avec la commande :

cat wikipedia.fr.txt.gz-part0* | gunzip > wikipedia.fr.txt

---------------------------------------

Voici la liste des commandes utilisées :

wget https://dumps.wikimedia.org/frwiki/latest/frwiki-latest-pages-articles-multistream.xml.bz2

(environ 5Go)

bzcat frwiki-latest-pages-articles-multistream.xml.bz2 | tr "\040\041\042\043\044\045\046\047\050\051\052\053\054\056\057\060\061\062\063\064\065\066\067\070\071\072\073\074\075\076\077\100\133\134\135\136\137\140\173\174\175\176" "\n" > toto

(cette commande dure environ 10mn sur mon PC à processeur 2CV génération 6, et le fichier toto fait environ 21Go. Le fichier a été nommé ainsi pour honorer la mémoire des enseignants qui m'ont formé. Les codes apparaissant en base octale dans cette commande sont listés en bas de ce readme)

cat toto | tr -s "\n" | awk '!x[$0]++' | sort > wikipedia.fr.txt

(cette commande dure environ 15mn et le fichier wikipedia.fr.txt fait 311Mo. La commande awk utilisée a été recommandée par https://github.com/TiJof en commentaire et est la cause de la perte de 5% de ma masse cérébrale... Elle remplace efficacement la "sort | uniq" utilisée auparavant et qui durait 1h30). Vous trouverez plus d'explications dans ce billet de blog : https://zythom.fr/2020/12/awk-awk-awk/.

wc -l wikipedia.fr.txt # la commande indique que le fichier fait 23 260 223 lignes
Le fichier wikipedia.fr.txt contient des mots aussi intéressants que "aaaaaaaaaaaaaaaaaaaargh" ou "Barthélémy-Louis-Charles". Amusez-vous bien.

gzip wikipedia.txt
split -d -b 20M wikipedia.fr.txt.gz wikipedia.fr.txt.gz-part

-------------------------------------

Notes : Pour information, voici la table des codes ASCII (en octal) utilisée pour générer le premier fichier toto

Octal Hex Caractère

----- --- ---------

040 20 SP (Space)

041 21 ! (exclamation mark)

042 22 " (double quote)

043 23 # (number sign)

044 24 $ (dollar sign)

045 25 % (percent)

046 26 & (ampersand)

047 27 ' (single quote)

050 28 ( (left opening parenthesis)

051 29 ) (right closing parenthesis)

052 2A * (asterisk)

053 2B + (plus)

054 2C , (comma)

--------------------------------

056 2E . (dot)

057 2F / (forward slash)

060 30 0

061 31 1

062 32 2

063 33 3

064 34 4

065 35 5

066 36 6

067 37 7

070 38 8

071 39 9

072 3A : (colon)

073 3B ; (semi-colon)

074 3C < (less than sign)

075 3D = (equal sign)

076 3E > (greater than sign)

077 3F ? (question mark)

100 40 @ (AT symbol)

--------------------------------

133 5B [ (left opening bracket)

134 5C \ (back slash)

135 5D ] (right closing bracket)

136 5E ^ (caret cirumflex)

137 5F _ (underscore)

140 60 ` (apostrophe du 7 ^^)

--------------------------------

173 7B { (left opening brace)

174 7C | (vertical bar)

175 7D } (right closing brace)

176 7E ~ (tilde)



