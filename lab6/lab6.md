### Problem 1
α) Υπολογίστε τις παραμέτρους ενός ζεύγους κλειδιών RSA κάνοντας τους υπολογισμούς με το «χέρι» με βάση τις παρακάτω τιμές:

p=7
q=11
n=;
φ(n)=;
e=13
d=;

Σημ. για τον υπολογισμό του d χρησιμοποιήστε τον εκτεταμένο αλγόριθμο του Ευκλείδη
(δείτε το Multiplicative-Inverse.xlsx)

β) Ποιοί από τους παραπάνω αριθμούς επιλέγονται τυχαία και ποιοί υπολογίζονται;

γ) Με ποιούς περιορισμούς επιλέγονται οι τυχαίοι αριθμοί;

#### Solution 1
a)

n=p*q=7*11

Φ(n)=(p-1)(q-1)=6*10

d=37

### Problem 2
α) Με τις τιμές e και d που βρήκατε στην προηγούμενη ερώτηση κρυπτογραφήστε τον αριθμό 5.

β) Στην συνέχεια αποκρυπτογραφήστε το αποτέλεσμα κρυπτογράφησης για επαλήθευση.
(θα πρέπει να βρείτε πάλι 5)

Για ευκολία στους υπολογισμούς (απο)-κρυπτογράφησης χρησιμοποιείστε το https://www.wolframalpha.com/.
#### Solution 2 
5^e=5^(13 mod 77) -> 26
26^d=26^(37 mod 77) -> 5

### Problem 3
α) Χρησιμοποιώντας το OpenSSL δημιουργήστε δύο ζεύγη κλειδιών (ιδιωτικό και δημόσιο) μήκους 1024bits και με δημόσιο κλειδί (public exponent) τον αριθμό e=7.
Το κάθε ζεύγος κλειδιών υποτίθεται ότι θα αντιστοιχεί σε διαφορετικό χρήστη με ονόματα Alice και Bob, επομένως θα πρέπει να ονομαστούν ως εξής:
- Ζεύγος κλειδιών της Alice: priv-A.pem και pub-A.pem
- Ζεύγος κλειδιών του Bob: priv-B.pem και pub-B.pem

β) Με την κατάλληλη εντολή openssl εμφανίστε το περιεχόμενο του ιδιωτικού κλειδιού της Alice και εντοπίστε το modulus n και το ιδιωτικό κλειδί d (private exponent).

γ) Με την κατάλληλη εντολή openssl εμφανίστε το περιεχόμενο του δημοσίου κλειδιού της Alice και εντοπίστε το modulus n.
- Η τιμή του public exponent είναι αυτή που ζητήσαμε (δηλ. e=7);
- Το modulus n είναι ίδιο με αυτό που βρήκατε και στην περίπτωση του ιδιωτικού κλειδιού;

#### Solution 3

```bash
openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:1024 -pkeyopt rsa_keygen_pubexp:3 -out privA.pem

openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:1024 -pkeyopt rsa_keygen_pubexp:3 -out privB.pem
```

### Problem 4
Θεωρήστε ότι η Alice θέλει να στείλει ένα κείμενο στον Bob με ασφάλεια χρησιμοποιώντας το OpenSSL.
α) Δημιουργείστε ένα δοκιμαστικό κείμενο με όνομα message.txt το οποίο θα πρέπει η Alice να κρυπτογραφήσει με τον αλγόριθμο RSA για να το στείλει στον Bob (με όνομα ciphertext).
- Ποιο κλειδί πρέπει να χρησιμοποιήσει η Alice;
- Καταγράψτε την εντολή της Alice.

β) Αποκρυπτογραφήστε το κρυπτογραφημένο αρχείο (ciphertext) (που "έλαβε" ο Bob) με όνομα received_message.txt
- Ποιο κλειδί πρέπει να χρησιμοποιήσει ο Bob;
- Καταγράψτε την εντολή του Bob.
- Είναι σίγουρος ο Bob ότι το μήνυμα που έλαβε έχει αποσταλεί από την Alice;

#### Solution 4
```bash
openssl pkey -in privA.pem -out pubA.pem -pubout

openssl pkey -in privB.pem -out pubB.pem -pubout

openssl pkey -in privA.pem -text

openssl pkey -in pubA.pem -pubin -text
```

### Problem 5
α) Για να μπορεί να επαληθευτεί η γνησιότητα του μηνύματος καθώς και του αποστολέα, η Alice δημιουργεί μια ψηφιακή υπογραφή του αρχικού κειμένου (message.txt) με τον digest αλγόριθμο sha256 και στέλνει το αρχείο της υπογραφής στον Bob (με όνομα αρχείου Alice-signature).
- Ποιο κλειδί πρέπει να χρησιμοποιήσει η Alice για την ψηφιακή υπογραφή;
- Καταγράψτε την εντολή της Alice.

β) Αντιγράψτε το αρχείο της ψηφιακής υπογραφής (Alice-signature) στον υποφάκελο του Bob.
- Ποιο κλειδί πρέπει να χρησιμοποιήσει ο Bob για τον έλεγχο της ψηφιακής υπογραφής;
- Καταγράψτε την εντολή του Bob.
- Τι θα συμβεί αν το μήνυμα που έλαβε ο Bob (received_message.txt) (ή το αρχείο της ψηφιακής υπογραφής) αλλάξει με οποιοδήποτε τρόπο;

#### Solution 5
C:\Users\kpapadak>openssl pkeyutl -encrypt -in message.txt -inkey pubB.pem -pubin -out cipher.bin
C:\Users\kpapadak>openssl pkeyutl -decrypt -in cipher.bin -inkey privB.pem -out rec_message.txt


C:\Users\kpapadak>openssl dgst -sha1 -sign privA.pem -out signature message.txt

C:\Users\kpapadak>openssl dgst -sha1 -verify pubA.pem -signature signature rec_message.txt
Verified OK
