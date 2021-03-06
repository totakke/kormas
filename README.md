# kormas

Utility functions for [Korma (A Clojure Library for Tasty SQL)][korma]

```
[kormas "0.1.0"]
```

## Usage

```clojure
(require '[kormas.core :refer [definit mysql-db-config]])
(require '[kormas.util :refer [swap transform-key]])
```

```clojure
(definit db-init
  [user password]

  ;; db
  (defdb main-db
    (mysql (mysql-db-config {:user user
                             :password password
                             :host "localhost"
                             :db "mydb"})))

  ;; entities
  (defentity myuser
    (database main-db)
    (prepare (fn [v]
               (-> v
                   (swap :status keyword)
                   (swap :enable #(= 0 %)))))
    (transform (fn [v]
                 (-> v
                     (swap :status str)
                     (swap :enable #(if % 0 1)))))))
```

## License

Copyright [Takashi AOKI][tak.sh]

Licensed under the [Apache License, Version 2.0][apache-license-2.0].

[korma]: http://sqlkorma.com/
[tak.sh]: http://tak.sh
[apache-license-2.0]: http://www.apache.org/licenses/LICENSE-2.0.html
