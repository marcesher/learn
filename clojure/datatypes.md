# Sets, atoms

```
(def people #{})
(conj people "marc")
people
;; #{}, because it's not updating in place. So:

(def new-people (conj people "marc"))

;; but better to use a reference type such as atom

(def people (atom #{}))
(swap! people conj "steve")
(deref people)
;; same as:

@people