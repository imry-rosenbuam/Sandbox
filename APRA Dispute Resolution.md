# Defaults 


The APRA Dispute Resolution mandate concerns up to 4 posssible entity slots:
+ Two parties the transaction (contraparty/counterparty)
+ Parents of each party

In ADEPT3 we provide the values for `covered-counterparty` , `covered-counterparty` and `foreign-covered-entity`
are valued provided by the taxonomy. However, in ADEPT 4 they are inferred from some atoms.

This default is related to the assumption that any input scenarios are concerning a product that is a `au-corporations-act/derivatives-contract`

```clojure
{"entity" [{"common" {"id" "booking-entity"
                      "bank-for-international-settlements" false
                      "central-bank" false}
            "relationship" {"parent" "none"}}
           {"common" {"id" "counterparty"
                      "bank-for-international-settlements" false
                      "central-bank" false}
            "relationship" {"parent" "none"}}]
 "transaction" {"role" {"counterparties" ["booking-entity" "counterparty"]}}
 "product" {"au-corporations-act"
            {"derivatives-contract" true}}}
```

# Mapping

## Entity

### Party

#### __Common__

+ `bank-for-international-settlements`: is NonApplicable if `covered-counterparty` is provided
+ `central-bank`: is NonApplicable if `covered-counterparty` is provided
+ `book-location`: is taken from `product.contrapartyBookLocation` and `product.counterpartyBookLocation`

#### __au-banking-act__

+ `adi`: is NonApplicable if `covered-entity` is provided
+ `authorised-banking-NOHC": is NonApplicable if `covered-entity` is provided
+ `covered-bond-special-purpose-vehicle`: is NonApplicable if `covered-counterparty` is provided

#### __au-foreign-corporations-act__
+ `foreign-corporation`: is NonApplicable if `foreign-covered-entity` is provided

#### __au-insurance-act__
+ `authorised-insurance-NOHC`: is NonApplicable if `covered-entity` is provided
+ `authorised-to-carry-insurance-foreign-country`: is NonApplicable if `covered-entity` is provided
+ `category-c-insurer` : is NonApplicable if `covered-entity` is provided
+ `foreign-general-insurer` : is NonApplicable if `covered-entity` is provided
+ `general-insurer` : is NonApplicable if `covered-entity` is provided

#### __au-life-insurance-act__
+ `eligible-foreign-life-insurance-company` : is NonApplicable if `covered-entity` is provided
+ `friendly-society` : is NonApplicable if `covered-entity` is provided
+ `life-company` : is NonApplicable if `covered-entity` is provided
+ `registered-life-NOHC` : is NonApplicable if `covered-entity` is provided

#### __au-superannuation-industry-supervision-act__
+ `approved-deposit-fund` is NonApplicable if `covered-entity` is provided  ( or `registrable-superannuation-entity`)
+ `pooled-superannuation-trust` is NonApplicable if `covered-entity` is provided  ( or `registrable-superannuation-entity`)
+ `registrable-superannuation-entity` is NonApplicable if `covered-entity` is provided
+ `regulated-superannuation-fund` is NonApplicable if `covered-entity` is provided ( or `registrable-superannuation-entity`)

#### __cps226__
+ `covered-entity` from `party.apraCoveredEntity`
+ `foreign-covered-entity` from `party.apraEligibleForeignCoveredEntity`
+ `covered-counterparty` from `party.apraCoveredCounterparty`
+ `collective-investment-vehicle-for-hedging-real-estate-or-infrastructure-asset`: is NonApplicable if `covered-counterparty` is provided
+ `financial-institution` : is NonApplicable if `covered-counterparty` is provided
+ `multilateral-development-bank` : is NonApplicable if `covered-counterparty` is provided
+ `public-sector-entity` : is NonApplicable if `covered-counterparty` is provided
+ `sovereign` : is NonApplicable if `covered-counterparty` is provided
+ `special-purpose-vehicle-for-hedging-real-estate-or-infrastructure-asset` : is NonApplicable if `covered-counterparty` is provided

### Parent

Nothing can be inferred from ADEPT 3

## Product

### __ISDA__
These are all one-to-one:

+ `asset-class` from trade.assetclass
+ `base-product` from trade.baseproduct

## Transaction

### __Common__
+ `centrally-cleared` mapped one-to-one from trade.intenttoclear