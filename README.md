# Computer Architecture Lab 3

## Ομάδα 11
### Καλαντζής Γεώργιος 8818 gkalantz@ece.auth.gr
### Κοσέογλου Σωκράτης 8837 sokrkose@ece.auth.gr

Σκοπός της συγκεκριμένης εργασίας είναι η εξοικείωση με το McPAT framework  , το οποίο μας δίνει την δυνατότητα να μοντελοποιούμε στις αρχιτεκτονικές μας ενεργειακές μετρικές, όπως energy-delay-area product (EDAP) και να μελετάμε διάφορα trade-offs στις σχεδιαστικές μας αποφάσεις.


#### Ερώτημα 1

#### A.

Στο συγκεκριμένο ερώτημα ζητείται να ανατρέξουμε στην βιβλιογραφία αναφορικά με τις απώλειες ισχύος σε ένα CMOS, έτσι ώστε να κατονοήσουμε καλύτερα τα αποτελέσματα του McPAT Simulator και πιο συγκεκριμένα, το **Dynamic Power** καθώς και το **Leakage** τα οποία δίνονται ως αποτελέσματα με το πέρας της κάθε προσομοίωσης. Αρχικά, οι συνολικές απώλειες ισχύος σε ένα CMOS είναι το άθροισμα της δυναμικής κατανάλωσης και της στατικής κατανάλωσης, δηλαδή, **P_total = P_dynamic + P_static**. Η δυναμική κατανάλωση με την σειρά της αποτελείτε από το άθροισμα των διακοπτικών απωλειών και το ρεύμα βραχυκυκλώματος, **P_dynamic = P_switcing + P_shortcircuit**. Ενώ οι στατικές απώλειες είναι αποτέλεσμα του **ρεύματος διαρροής υποκατωφίου** καθώς και του **ρεύματος διαρροής της πύλης**, δηλαδή δίνεται από τον τύπο **P_static = (I_sub + I_gate)\*Vdd** . Ας πάμε λοιπόν να αναλύσουμε πιο συγκεκριμένα όλες τις παραπάνω απώλειες ισχύος.

* Dynamic Power Dissipation

  * Switching

  * Short Circuit


* Static Power Dissipation

  * Subthreshold Leakage Current

  * Gate Leakage Current


* Switching : Ορίζεται ως η απώλεια ισχύος που οφείλεται στην φόρτιση και στην εκφόρτιση της πύλης του τρανζίστορ κατά την μετάδοση του σήματος και εξάρταται εκτός των υπολοίπων από την συχνότητα του ρολογιού και ενός παράγοντα μεταγωγής a.

* Short Circuit : Οφείλεται στο σταθερό DC ρεύμα που εμφανίζεται στο CMOS κατά την μετάβαση σήματος όταν το σήμα εισόδου αλλάζει τάση.

* Subthreshold Leakage Current : Οφείλεται στο ρεύμα που διαρρέεται κατα την διάρκεια της περιοχής αποκοπής του τρανζίστορ.

* Gate Leakage Current : Οφείλεται στο ρεύμα που διαρρέται από την πύλη οξειδίου


Αρχικά η διαρροή δυναμικής ισχύος είναι ανάλογη του συνολικού φορτίου χωρητικότητας, της τάσης τροφοδοσίας , της αλλαγής τάσης κατά την μεταγωγή , της συχνότητας του ρολογιού και της ενός παράγοντα μεταγωγής/δραστηριότητας όπως ανέφερα και παραπάνω. Ο παράγοντας αυτός οφείλεται στα στατιστικά των προσβάσεων τα οποία μας παρέχονται από την προσομοίωση της αρχιτεκτονικής.

Η διαρροή στατικής ισχύος εξαρτάται από το μέγεθος των τρανζίστορ και την τοπική κατάσταση των συσκεύων.

Άρα άμα εκτελέσω διαφορετικά προγράμματα πάνω στον ίδιο επεξεργαστή αυτό που θα επηρεαστεί θα είναι η διαρροή δυναμικής ισχύος , αφού είναι ανάλογη των προσβάσεων (accesses) για παράδειγμα στις caches και σε άλλα στοιχεία της αρχιτεκτονικής. Δεν έχει άμεσα σημασία η χρονική διάρκεια εκτέλεσης ενός προγράμματος , δίοτι δεν είναι απαραίτητο ότι ένα "χρονοβόρο" πρόγραμμα θα απαιτεί και μεγαλό αριθμό προσβάσεων από το υλικό της αρχιτεκτονικής του υπολογιστή (πχ RAM, caches, branch predictors, περιεφερειακα).


#### B.

Αρχικά, δίνεται ότι η στιγμιαία ισχύς που καταναλώνει ο **επεξεργαστής Α** είναι **4W**, ενω η στιγμιαία ισχύς του **επεξεργαστή Β** είναι **40W**, δηλαδή **10 φορές μεγαλύτερη**, συνεπώς δεδομένου ότι οι δύο επεξεργαστές τρέχουν το ίδιο πρόγραμμα και με την ίδια ταχύτητα (δηλαδή έχουν ίδια χρονική διάρκεια, memory accesses, committed instructions κλπ), τότε είναι φανερό ότι ο επεξεργαστής Β θα καταναλώνει **10 φορές περισσότερη ενέργεια** από μια μπαταρία σε σχέση με τον επεξεργαστή Α. Στην περίπτωση όμως όπου ο επεξεργαστής Β ναι μεν τρέχει το ίδιο πρόγραμμα με τον Α αλλά είναι **αρκετά γρηγορότερος** (και συγκεκριμένα 10 φορές γρηγορότερος), δηλαδή τρέχει το ίδιο πρόγραμμα σε **μικρότερη χρονική διάρκεια**, και πιο συγκεκριμένα εαν τρέχει σε 10 φορές μικρότερο χρόνο απ' ότι τρέχει το ίδιο πρόγραμμα ο επεξεργαστής Α, τότε η κατανάλωση ενέργειας από μια μπαταρία θα είναι μικρότερη για τον επεξεργαστή Β, καθώς η συνολική ενέργεια μιας μπαταρίας δίνεται από τις συνολικές **Whs (Watt-hours)** που μπορεί να τροφοδοτεί ένα σύστημα, δηλαδή είναι το γινόμενο **Watt\*Time**. Τέλος, εαν τα προγράμματα τα οποία τρέχουν οι δυο επεξεργαστές είναι διαφορετικά δεν μπορούμε να βγάλουμε κάποιο συμπέρασμα για την κατανάλωση ενέργειας από μια μπαταρία δεδομένου ότι λείπουν αρκετά δεδομένα τα οποία χρειαζόμαστε.

To McPAT δίνει ως αποτελέσματα κάποια ενεργειακά δεδομένα του εκάστοτε επεξεργαστή, συνεπώς όπως είπαμε και προηγουμένως, δεν μπορούμε να βγάλουμε κάποιο σίγουρο συμπέρασμα σχετικά με την διάρκεια της μπαταρίας του κάθε επεξεργαστικού συστήματος. Για να μπορέσουμε να βγάλουμε συμεράσματα όσον αφορά την διάρκεια της μπαταρίας, θα πρέπει να γνωρίζουμε περισσότερα πράγματα για το πρόγραμμα το οποίο τρέχει ο κάθε επεξεργαστής, με κυριότερη μεταβλητή τον **χρόνο εκτέλεσης** του κάθε προγράμματος.

#### Γ.

Αρχικά, στον παρακάτω πίνακα φαίνονται τα συνοπτικά αποτελέσματα των δυο προσομοιώσεων.

|           |   Area     |   Peak Power   |   Total Leakage   |   Peak Dynamic   |   Subthreshold Leakage  | Subthreshold Leakage with Power Gating|    Gate Leakage   |   Runtime Dynamic    |
|-----------|------------|----------------|-------------------|------------------|-------------------------|------------------|----------------------|----------------|
|  Xeon     | 410.507mm^2| 134.938 W       | 36.8319 W          | 98.1063 W         | 35.1632 W                | 16.3977 W         |  1.66871 W        | 72.9199 W    |
|ARM A9 2GHz| 5.39698 mm^2| 1.74189 W       | 0.108687 W          | 1.6332 W         | 0.0523094 W             |   -------------   | 0.0563774 W        |  2.96053 W   |
