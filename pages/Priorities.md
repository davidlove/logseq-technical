# Waiting
	- {{query (todo waiting))}}
- # Notes Review
	- #+BEGIN_QUERY
	  {:title "Notes Reviews (Non-Scheduled)"
	  :query [:find (pull ?b [*])
	  :where
	  [?b :block/ref-pages ?p]
	  [?p :block/name "schedule"]
	  [?b :block/marker ?m]
	  [(contains? #{"TODO" "LATER" "DOING" "NOW"} ?m)]
	  [(missing? $ ?b :block/scheduled)]
	  [(missing? $ ?b :block/deadline)]
	  ]
	  :breadcrumb-show? true
	  }
	  #+END_QUERY
- # A
	- query-table:: false
	  #+BEGIN_QUERY
	  {:title "Non-Scheduled Priority A"
	  :query [:find (pull ?b [*])
	  :where
	  [?b :block/marker ?m]
	  [?b :block/priority "A"]
	  [(contains? #{"TODO" "LATER" "DOING" "NOW"} ?m)]
	  [(missing? $ ?b :block/scheduled)]
	  [(missing? $ ?b :block/deadline)]
	  ]
	  :breadcrumb-show? true
	  }
	  #+END_QUERY
	- #+BEGIN_QUERY
	  {:title "Scheduled Priority A"
	  :query [:find (pull ?b [*])
	  :where
	  [?b :block/marker ?m]
	  [?b :block/priority "A"]
	  [(contains? #{"TODO" "LATER" "DOING" "NOW"} ?m)]
	  ]
	  :breadcrumb-show? true
	  :collapsed? true
	  }
	  #+END_QUERY
# B
	- #+BEGIN_QUERY
	  {:title "Non-Scheduled Priority B"
	  :query [:find (pull ?b [*])
	  :where
	  [?b :block/marker ?m]
	  [?b :block/priority "B"]
	  [(contains? #{"TODO" "LATER" "DOING" "NOW"} ?m)]
	  [(missing? $ ?b :block/scheduled)]
	  [(missing? $ ?b :block/deadline)]
	  ]
	  :breadcrumb-show? true
	  }
	  #+END_QUERY
	- #+BEGIN_QUERY
	  {:title "Scheduled Priority B"
	  :query [:find (pull ?b [*])
	  :where
	  [?b :block/marker ?m]
	  [?b :block/priority "B"]
	  [(contains? #{"TODO" "LATER" "DOING" "NOW"} ?m)]
	  ]
	  :breadcrumb-show? true
	  :collapsed? true
	  }
	  #+END_QUERY
# C
	- #+BEGIN_QUERY
	  {:title "Non-Scheduled Priority C"
	  :query [:find (pull ?b [*])
	  :where
	  [?b :block/marker ?m]
	  [?b :block/priority "C"]
	  [(contains? #{"TODO" "LATER" "DOING" "NOW"} ?m)]
	  [(missing? $ ?b :block/scheduled)]
	  [(missing? $ ?b :block/deadline)]
	  ]
	  :breadcrumb-show? true
	  }
	  #+END_QUERY
	- #+BEGIN_QUERY
	  {:title "Scheduled Priority C"
	  :query [:find (pull ?b [*])
	  :where
	  [?b :block/marker ?m]
	  [?b :block/priority "C"]
	  [(contains? #{"TODO" "LATER" "DOING" "NOW"} ?m)]
	  ]
	  :breadcrumb-show? true
	  :collapsed? true
	  }
	  #+END_QUERY
# No Priority
	- {{query (and (todo todo doing now later) (not (priority a b c)))))}}