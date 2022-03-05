- ```
  [
   {:title "📓 Notes Reviews (Non-Scheduled)"
    :query [:find (pull ?b [*])
            :where
            [?b :block/ref-pages ?p]
            [?p :block/name "daily notes"]
            [?b :block/marker ?m]
            [(contains? #{"TODO" "LATER" "DOING" "NOW"} ?m)]
            [(missing? $ ?b :block/scheduled)]
            [(missing? $ ?b :block/deadline)]
            ]
    :collapsed? true
    :breadcrumb-show? true
    }
   {:title      "🔥 OVERDUE"
    :query      [:find (pull ?b [*])
                 :in $ ?start ?next
                 :where
                 [?b :block/marker ?marker]
                 (or [?b :block/scheduled ?d]
                 [?b :block/deadline ?d])
                 [(contains? #{"TODO" "DOING" "NOW" "LATER" "WAITING"} ?marker)]
                 [(>= ?d ?start)]
                 [(<= ?d ?next)]]
    :inputs     [:365d :1d]
    :result-transform (fn [result]
                             (sort-by (fn [h]
                                   (get h :block/priority "Z")) result))
    :collapsed? false
    :breadcrumb-show? true}
   {:title      "🔨  Today"
    :query      [:find (pull ?b [*])
                 :in $ ?start ?next
                 :where
                 [?b :block/marker ?marker]
                 (or [?b :block/scheduled ?d]
                 [?b :block/deadline ?d])
                 [(contains? #{"TODO" "DOING" "NOW" "LATER" "WAITING"} ?marker)]
                 [(>= ?d ?start)]
                 [(< ?d ?next)]]
    :inputs     [:today :1d-after]
    :result-transform (fn [result]
                             (sort-by (fn [h]
                                   (get h :block/priority "Z")) result))
    :collapsed? false
    :breadcrumb-show? true}
   {:title      "🌄 Tomorrow"
    :query      [:find (pull ?b [*])
                 :in $ ?start ?next
                 :where
                 [?b :block/marker ?marker]
                 (or [?b :block/scheduled ?d]
                 [?b :block/deadline ?d])
                 [(contains? #{"TODO" "DOING" "NOW" "LATER" "WAITING"} ?marker)]
                 [(> ?d ?start)]
                 [(<= ?d ?next)]]
    :inputs     [:today :1d-after]
    :result-transform (fn [result]
                             (sort-by (fn [h]
                                   (get h :block/priority "Z")) result))
    :collapsed? true
    :breadcrumb-show? true}
   {:title      "📅 Following Week"
    :query      [:find (pull ?b [*])
                 :in $ ?start ?next
                 :where
                 [?b :block/marker ?marker]
                 (or [?b :block/scheduled ?d]
                 [?b :block/deadline ?d])
                 [(contains? #{"TODO" "DOING" "NOW" "LATER" "WAITING"} ?marker)]
                 [(> ?d ?start)]
                 [(<= ?d ?next)]]
    :inputs     [:tomorrow :7d-after]
    :result-transform (fn [result]
                             (sort-by (fn [h]
                                   (get h :block/priority "Z")) result))
    :collapsed? true
    :breadcrumb-show? true}
   {:title "🚨 Non-Scheduled Priority A"
    :query [:find (pull ?b [*])
            :where
            [?b :block/marker ?m]
            [?b :block/priority "A"]
            [(contains? #{"TODO" "LATER" "DOING" "NOW"} ?m)]
            [(missing? $ ?b :block/scheduled)]
            [(missing? $ ?b :block/deadline)]
            ]
    :collapsed? true
    :breadcrumb-show? true
    }
   {:title            "🔨 NOW"
    :query            [:find (pull ?h [*])
                       :in $ ?start ?today
                       :where
                       [?h :block/marker ?marker]
                       [(contains? #{"NOW" "DOING"} ?marker)]
                       [?h :block/page ?p]
                       [?p :block/journal? true]
                       [?p :block/journal-day ?d]
                       [(>= ?d ?start)]
                       [(<= ?d ?today)]]
    :inputs           [:14d :today]
    :result-transform (fn [result]
                        (sort-by (fn [h]
                                   (get h :block/priority "Z")) result))
    :collapsed?       false}
   {:title      " 📅 NEXT"
    :query      [:find (pull ?h [*])
                 :in $ ?start ?next
                 :where
                 [?h :block/marker ?marker]
                 [(contains? #{"NOW" "LATER" "TODO"} ?marker)]
                 [?h :block/ref-pages ?p]
                 [?p :block/journal? true]
                 [?p :block/journal-day ?d]
                 [(> ?d ?start)]
                 [(< ?d ?next)]]
    :inputs     [:today :7d-after]
    :collapsed? false}
   ]
  
  ```
- #+BEGIN_QUERY
   {:title "📓 Notes Reviews (Non-Scheduled)"
    :query [:find (pull ?b [*])
            :where
            [?b :block/ref-pages ?p]
            [?p :block/name "daily notes"]
            [?b :block/marker ?m]
            [(contains? #{"TODO" "LATER" "DOING" "NOW"} ?m)]
            [(missing? $ ?b :block/scheduled)]
            [(missing? $ ?b :block/deadline)]
            ]
    :collapsed? true
    :breadcrumb-show? true
    }
  #+END_QUERY
- #+BEGIN_QUERY
   {:title      "🔥 OVERDUE"
    :query      [:find (pull ?b [*])
                 :in $ ?start ?next
                 :where
                 [?b :block/marker ?marker]
                 (or [?b :block/scheduled ?d]
                 [?b :block/deadline ?d])
                 [(contains? #{"TODO" "DOING" "NOW" "LATER" "WAITING"} ?marker)]
                 [(>= ?d ?start)]
                 [(<= ?d ?next)]]
    :inputs     [:365d :1d]
    :result-transform (fn [result]
                             (sort-by (fn [h]
                                   (get h :block/priority "Z")) result))
    :collapsed? false
    :breadcrumb-show? true}
  #+END_QUERY
- #+BEGIN_QUERY
   {:title      "⚒  Today"
    :query      [:find (pull ?b [*])
                 :in $ ?start ?next
                 :where
                 [?b :block/marker ?marker]
                 (or [?b :block/scheduled ?d]
                 [?b :block/deadline ?d])
                 [(contains? #{"TODO" "DOING" "NOW" "LATER" "WAITING"} ?marker)]
                 [(>= ?d ?start)]
                 [(< ?d ?next)]]
    :inputs     [:today :1d-after]
    :result-transform (fn [result]
                             (sort-by (fn [h]
                                   (get h :block/priority "Z")) result))
    :collapsed? false
    :breadcrumb-show? true}
  #+END_QUERY
- #+BEGIN_QUERY
   {:title      "🌄 Tomorrow"
    :query      [:find (pull ?b [*])
                 :in $ ?start ?next
                 :where
                 [?b :block/marker ?marker]
                 (or [?b :block/scheduled ?d]
                 [?b :block/deadline ?d])
                 [(contains? #{"TODO" "DOING" "NOW" "LATER" "WAITING"} ?marker)]
                 [(> ?d ?start)]
                 [(<= ?d ?next)]]
    :inputs     [:today :1d-after]
    :result-transform (fn [result]
                             (sort-by (fn [h]
                                   (get h :block/priority "Z")) result))
    :collapsed? true
    :breadcrumb-show? true}
  #+END_QUERY
- #+BEGIN_QUERY
   {:title      "📅 Following Week"
    :query      [:find (pull ?b [*])
                 :in $ ?start ?next
                 :where
                 [?b :block/marker ?marker]
                 (or [?b :block/scheduled ?d]
                 [?b :block/deadline ?d])
                 [(contains? #{"TODO" "DOING" "NOW" "LATER" "WAITING"} ?marker)]
                 [(> ?d ?start)]
                 [(<= ?d ?next)]]
    :inputs     [:tomorrow :7d-after]
    :result-transform (fn [result]
                             (sort-by (fn [h]
                                   (get h :block/priority "Z")) result))
    :collapsed? true
    :breadcrumb-show? true}
  #+END_QUERY