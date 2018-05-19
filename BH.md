          ---------------------------------------------------------------------------------------------------------------------------------
                name:  <unnamed>
                 log:  C:\Users\nate\Dropbox\Paper Trust and Inequality\Current Version\Breznau and Hommerich Liberalization and Public Support of Social Welfare Policy\IJSW\Final\BH.smcl
            log type:  smcl
           opened on:  19 May 2018, 13:04:34

          . pwcorr govwelf govprices govhealth govold govunemp govjobs

                       |  govwelf govpri~s govhea~h   govold govunemp  govjobs
          -------------+------------------------------------------------------
               govwelf |   1.0000 
             govprices |   0.6568   1.0000 
             govhealth |   0.7814   0.3677   1.0000 
                govold |   0.8045   0.3592   0.6083   1.0000 
              govunemp |   0.6306   0.3037   0.3270   0.3811   1.0000 
               govjobs |   0.6898   0.4471   0.3419   0.3510   0.4136   1.0000 

          . alpha govjobs govprices govhealth govold govunemp

          Test scale = mean(unstandardized items)

          Average interitem covariance:     .2232241
          Number of items in the scale:            5
          Scale reliability coefficient:      0.7272

          . reg govwelf govjobs_i govprices_i govhealth_i govold_i govunemp_i, beta

                Source |       SS           df       MS      Number of obs   =    85,577
          -------------+----------------------------------   F(5, 85571)     =         .
                 Model |   64080.044         5  12816.0088   Prob > F        =         .
              Residual |           0    85,571           0   R-squared       =    1.0000
          -------------+----------------------------------   Adj R-squared   =    1.0000
                 Total |   64080.044    85,576  .748808592   Root MSE        =         0

          ------------------------------------------------------------------------------
               govwelf |      Coef.   Std. Err.      t    P>|t|                     Beta
          -------------+----------------------------------------------------------------
             govjobs_i |    .237765          .        .       .                 .2652486
           govprices_i |   .2440909          .        .       .                 .2272146
           govhealth_i |   .4700325          .        .       .                 .3220384
              govold_i |   .5072493          .        .       .                 .3507833
            govunemp_i |   .2153113          .        .       .                 .2101845
                 _cons |  -5.638402          .        .       .                        .
          ------------------------------------------------------------------------------


          . factor govjobs_i govprices_i govhealth_i govold_i govunemp_i, pcf
          (obs=85,577)

          Factor analysis/correlation                      Number of obs    =     85,577
              Method: principal-component factors          Retained factors =          1
              Rotation: (unrotated)                        Number of params =          5

              --------------------------------------------------------------------------
                   Factor  |   Eigenvalue   Difference        Proportion   Cumulative
              -------------+------------------------------------------------------------
                  Factor1  |      2.58041      1.75374            0.5161       0.5161
                  Factor2  |      0.82667      0.12856            0.1653       0.6814
                  Factor3  |      0.69812      0.18668            0.1396       0.8210
                  Factor4  |      0.51143      0.12807            0.1023       0.9233
                  Factor5  |      0.38337            .            0.0767       1.0000
              --------------------------------------------------------------------------
              LR test: independent vs. saturated:  chi2(10) = 1.1e+05 Prob>chi2 = 0.0000

          Factor loadings (pattern matrix) and unique variances

              ---------------------------------------
                  Variable |  Factor1 |   Uniqueness 
              -------------+----------+--------------
                 govjobs_i |   0.7090 |      0.4973  
               govprices_i |   0.6857 |      0.5299  
               govhealth_i |   0.7539 |      0.4317  
                  govold_i |   0.7707 |      0.4060  
                govunemp_i |   0.6673 |      0.5547  
              ---------------------------------------

          . predict govwelfa
          (regression scoring assumed)

          Scoring coefficients (method = regression)

              ------------------------
                  Variable |  Factor1 
              -------------+----------
                 govjobs_i |  0.27476 
               govprices_i |  0.26572 
               govhealth_i |  0.29216 
                  govold_i |  0.29867 
                govunemp_i |  0.25861 
              ------------------------


          . pwcorr govwelf govwelfa

                       |  govwelf govwelfa
          -------------+------------------
               govwelf |   1.0000 
              govwelfa |   0.9972   1.0000 

          . preserve

          . collapse govjobs_i govprices_i govhealth_i govold_i govunemp_i countryx, by(cyear)

          . sum govjobs_i-govunemp_i

              Variable |        Obs        Mean    Std. Dev.       Min        Max
          -------------+---------------------------------------------------------
             govjobs_i |        105     3.05333    .4308457   2.159225    3.85225
           govprices_i |         61    3.242368    .2317916   2.729387   3.700953
           govhealth_i |         61    3.604725    .1979127   3.118187   3.890616
              govold_i |         61    3.569819    .1888804   3.165431   3.853833
            govunemp_i |         61    2.932796    .2893066    2.41252   3.509394

          . gen i1 = govprices_i -3.2419
          (44 missing values generated)

          . gen i2 = govhealth_i -3.6053
          (44 missing values generated)

          . gen i3 = govold_i -3.5707
          (44 missing values generated)

          . gen i4 = govunemp_i -2.9306
          (44 missing values generated)

          . gen i5 = govjobs_i -3.0512

          . replace i1=i1-0.01959
          (61 real changes made)

          . replace i2=i2-0.01365
          (61 real changes made)

          . replace i3=i3-0.00739
          (61 real changes made)

          . replace i4=i4-0.044
          (61 real changes made)

          . replace i5=i5-0.045907
          (105 real changes made)

          . collapse i1-i5, by(country)

          . sum i1-i5

              Variable |        Obs        Mean    Std. Dev.       Min        Max
          -------------+---------------------------------------------------------
                    i1 |         31   -.0228599     .225025  -.4314776   .3868583
                    i2 |         31   -.0125474    .1727555  -.4717628   .2381821
                    i3 |         31   -.0103527    .1721044  -.4066828   .2597702
                    i4 |         31   -.0049815    .2616371  -.5455747   .4813839
                    i5 |         34     .006103    .3762413  -.8375556   .5356748

          . log close
                name:  <unnamed>
                 log:  C:\Users\nate\Dropbox\Paper Trust and Inequality\Current Version\Breznau and Hommerich Liberalization and Public Support of Social Welfare Policy\IJSW\Final\BH.smcl
            log type:  smcl
           closed on:  19 May 2018, 13:04:36
          ---------------------------------------------------------------------------------------------------------------------------------
