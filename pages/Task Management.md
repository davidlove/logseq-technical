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
  {:title      "📅 Today"
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
  {:title      "📅 Tomorrow"
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
                                     (get h :block/scheduled "Z")) result))
      :collapsed? true
      :breadcrumb-show? true}
  #+END_QUERY