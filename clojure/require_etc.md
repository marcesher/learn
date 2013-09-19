(require 'some.package)
(some.package/boo 10)

(refer 'some.package)
(boo 10)

(use 'some.package) ;; require and refer all in one
(boo 10)

(use :reload 'some.package) ;; reloads every time without restarting repl

(doc str) ;; show docs

(source map) ;; show the source of a function

(ancestors (class [1 2 3])) ;; spits out a class hierarchy (ish... it ain't pretty)