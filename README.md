[![Build Status](https://travis-ci.org/Funz/plugin-Cristal.png)](https://travis-ci.org/Funz/plugin-Cristal)

# Funz plugin: Cristal

This plugin is dedicated to launch Cristal (V1 and V2, raw or xml available at http://oecd-nea.org/tools/abstract/detail/nea-1903/ ) calculations from Funz.
It supports the following syntax and features:

  * Input
    * file type supported: *.R, any other format for resources
    * parameter syntax: 
      * variable syntax: `$(...)`
      * formula syntax: `@{...}`
      * comment char: `*`
    * example input file:
        ```
        DEBUT_APOLLO2
        ...
        *Umetal
        nom_mil = 'FISSIL Umetal ' ;
        TOPT.'STMIL'.nom_mil = TABLE: ;
        TOPT.'STMIL'.nom_mil.'U238    ' = 2.49865E-03 ;
        TOPT.'STMIL'.nom_mil.'U235    ' = 4.49988E-02 ;
        TOPT.'STMIL'.nom_mil.'U234    ' = 4.91895E-04 ;
        TOPT.'STMIL'.nom_mil.'TEMPERATURE' = 21.0 ;
        WRITE: TOPT.'RESU' 'Umetal X:U C(X)=18742  H/X=0 ' ;
        WRITE: TOPT.'RESU' 'U=235.19021 ' ;
        *
        ...
        FIN_APOLLO2                                                         
        
        DEBUT_MORET
        TITRE Installation
        
        ARRE
          ETAP
            ACTI 100
            PASS 3
          KEFF
            SIGM 0.001
        FARR
        
        GEOM
        MODU 0
        TYPE 1 SPHE $(r~8.741)
        * Volume : Ext0 (LATEC name) 
        VOLU Ext0 0 1 1 0.0 0.0 0.0
        
        FINM
        FING
        
        CHIM
          MULT
        * Umetal
          APO2 1 NORD 1 
        FINC
        
        SOUR
        POIN 1000
          MODU 0
          VOLU Ext0 0.0 0.0 0.0
        FPOI
        FINS
        
        FIND
        FIN_MORET
        ```
      * will identify input:
        * r, with expected value of 8.741

  * Output
    * file type supported: *.listing
    * read `keff`/`mean_keff`, `sigma_keff`, `kinf`, `slowing_down`, `M2`, `B2`, `dimension`, `cx`, `hx`, `dkeff_pertu`, ...
    * example output file:
        ```
        ...
        ########################################################################################################################
        ########################################################################################################################
        ##                                                                                                                    ##
        ##                                             ESTIMATION FINALE DU KEFF                                              ##
        ##                                                                                                                    ##
        ##                                                          KEFF     ECART TYPE    INTERVALLE A +/- 3 SIGMA           ##
        ##                 ETAPE    492  ESTI. + FAIBLE SIGMA     0.99410 +/-  0.00100  :  0.99111 < KEFF < 0.99709           ##
        ##                                                                                                                    ##
        ##                               COMBI. GENERALE          0.99410 +/-  0.00100  :  0.99111 < KEFF < 0.99709           ##
        ...
        ```
      * will return output:
        * mean_keff=0.99410
        * sigma_keff=0.00100


![Analytics](https://ga-beacon.appspot.com/UA-109580-20/plugin-Cristal)
