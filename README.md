# utl-inverse-probabilty-weighting-iptw-covariance-balancing-multinomial-case-r-weightit
Inverse probabilty weighting iptw covariance balancing multinomial case r weightit
    %let pgm=utl-inverse-probabilty-weighting-iptw-covariance-balancing-multinomial-case-r-weightit;

    %stop_submission;

    Inverse probabilty weighting iptw covariance balancing multinomial case r weightit

    The binary case is much simpler?

    CONTENTS
        1 r weightit solution
        2 Key components explained
        3 covariance, propensity instumental

    I am out of my confort zone for this mutinomial treament problem

    https://tinyurl.com/5n72ux3s
    https://github.com/rogerjdeangelis/utl-inverse-probabilty-weighting-iptw-covariance-balancing-multinomial-case-r-weightit

    hi res love plot
    https://tinyurl.com/4bsu2ndx
    https://github.com/rogerjdeangelis/utl-inverse-probabilty-weighting-iptw-covariance-balancing-multinomial-case-r-weightit/blob/main/balance.pdf

    Problem Balance the Covaiance of the independent variables
    -----------------------------------------------------------

    Note the SMD is closer to reference rangge then the unadjusted.

                           Covariance Balance
                      Standardized Mean Differences
         -0.2  -0.1  0.0  +0.1  0.2        0.4        0.6        0.8
          -+----------+----------+----------+----------+----------+--
          |      |    |     | Standardized Mean Differences         |
          |      |Adj |UnAdj| Measure UnAdj      Adj                |
     sex  +      |-.03|  .06| prop    0.589     0.067               +
          |      |    |     | age     0.625     0.161               |
          |      |    |     | sex     0.064    -0.034               |
          |      |    |     |                                       |
          |      |    |     |                                       |
          |      |    |  Adj|                       UnAdj           |
     prop +      |    |  .07|                         .58           +
          |      |    |     |                                       |
          |      |    |     | Samples    Control Treated            |
          |      |    |     | Unweighted   52     148               |
          |      |    |     | Weighted     46     144               |
          |      |    |     |                                       +
          |      |    |     |  Adj                    Unadj         |
     age  +      |    |     |  .16                      .62         |
          |      |    |     |                                       |
          |      |Accepted  |                                       |
          |      |Range     |                                       |
          |      | +/- 0.1  |                                       |
          |      |<-------->|                                       |
    B     -+----------+----------+----------+----------+----------+--
         -0.2  -0.1  0.0  +0.1  0.2        0.4        0.6        0.8
                      Standardized Mean Differences

    Other tools for reducing confoundiing

    Propensity related
    -----------------------------------------------------------------------------------------------------------------------------------
    https://github.com/rogerjdeangelis/utl-propensity-score-matching-sas-psmatch-r-psm-package-matchit
    https://github.com/rogerjdeangelis/utl-select-equal-size-samples-from-NY-voters-where-age-and-gender-are-equal-propensity-scoring
    https://github.com/rogerjdeangelis/utl_propensity_for_students_to_be_in_the_same_classes

    Instumental Variables Related
    ----------------------------------------------------------------------------------------------------------------------------------
    Related Unstrumental Varables
    https://github.com/rogerjdeangelis/utl-using-instrumental-variables-to-more-precisely-predict-the-income-of-vietnam-veterans

    sas communities
    https://tinyurl.com/3w44m5d2
    https://communities.sas.com/t5/Statistical-Procedures/Assessing-Balance-after-IPTW/m-p/748221#M36397

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */
    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
      input age sex trt wgt @@;
    cards4;
    44 1 1 154  44 1 1 154  33 1 1 139 53 1 1 177  60 0 1 182 43 0 0 137 43 1 1 159  58 0 1 186
    48 0 1 156  48 0 1 156  58 0 1 202 50 0 0 160  47 1 0 154 53 0 1 163 52 1 0 155  58 0 1 170
    66 1 1 169  66 1 1 169  52 0 0 152 50 0 1 174  38 0 1 155 48 0 1 178 51 0 1 172  53 1 1 174
    51 1 1 160  51 1 1 160  39 0 1 175 64 0 1 191  52 0 1 176 47 0 0 154 40 1 0 134  40 1 1 152
    51 0 1 178  51 0 1 178  63 1 1 158 48 0 0 157  49 1 1 156 40 0 1 145 49 0 1 164  49 1 1 175
    67 0 1 171  67 0 1 171  54 1 1 162 65 1 1 149  50 0 0 150 50 0 1 169 64 1 1 180  47 1 1 143
    55 1 1 161  55 1 1 161  47 1 0 141 35 1 0 136  54 1 1 167 42 1 1 143 55 1 0 139  56 1 1 165
    37 0 0 145  37 0 0 145  59 0 1 182 56 1 1 161  46 0 0 160 33 1 1 123 50 0 1 156  46 1 0 131
    43 0 1 158  43 0 1 158  59 1 1 159 51 0 1 174  56 1 0 148 46 1 1 158 46 1 0 137  60 1 1 168
    46 1 1 158  46 1 1 158  58 0 1 178 52 0 1 169  48 1 0 145 59 0 1 178 29 0 1 169  46 0 1 160
    62 0 1 187  62 0 1 187  57 1 1 156 54 1 0 153  53 0 1 181 44 0 1 163 61 1 1 179  61 0 1 172
    54 1 1 166  54 1 1 166  56 0 0 163 45 0 0 141  61 0 1 190 56 0 1 178 35 0 0 147  40 1 1 155
    54 0 1 181  54 0 1 181  49 0 0 160 47 0 1 172  54 1 1 159 34 1 1 153 57 1 0 151  37 1 1 137
    51 0 0 150  51 0 0 150  47 0 0 125 40 0 0 136  47 0 1 183 49 0 0 152 69 1 1 173  82 0 1 217
    44 0 1 160  44 0 1 160  46 0 1 179 39 1 1 138  61 1 1 168 55 1 1 159 36 0 1 154  46 1 1 144
    68 0 1 161  68 0 1 161  43 0 1 151 53 0 1 185  60 1 1 169 53 0 1 166 57 1 0 144  53 1 1 164
    55 1 0 144  55 1 0 144  48 1 1 162 54 0 0 162  55 0 1 190 51 0 1 170 47 0 1 163  56 0 1 182
    30 0 0 135  30 0 0 135  37 1 0 134 51 1 1 178  52 0 1 185 44 1 1 157 34 1 1 151  45 1 1 161
    57 0 0 162  57 0 0 162  72 0 1 190 59 0 1 180  44 1 1 143 42 0 0 131 35 0 1 143  55 1 1 162
    45 0 1 160  45 0 1 160  62 1 1 166 71 1 1 192  64 0 1 175 40 1 1 148 34 1 1 153  54 1 1 164
    39 1 0 147  39 1 0 147  39 1 1 150 45 0 1 185  44 1 1 140 51 0 1 181 45 1 1 163  48 1 0 147
    48 1 0 141  48 1 0 141  46 1 1 160 27 1 1 134  72 0 1 194 41 0 0 139 35 0 0 123  51 1 1 146
    40 1 0 131  40 1 0 131  45 0 1 174 60 0 1 167  65 0 1 187 45 0 0 138 57 1 1 173  50 1 1 152
    43 0 1 175  43 0 1 175  58 0 1 157 43 1 1 151  48 1 1 161 47 0 0 145 71 1 1 205  71 0 1 194
    44 1 1 147  44 1 1 147  49 1 1 143 43 1 1 151  40 1 1 155 68 1 1 190 37 0 0 132  43 1 1 148
    ;;;;
    run;quit;

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    proc datasets lib=work nodetails nolist;
     delete want;
    run;quit;

    %utlflkil(d:/pdf/balance.pdf);

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(WeightIt)
    library(cobalt)
    source("c:/oto/fn_tosas9x.R")
    options(sqldf.dll = "d:/dll/sqlean.dll")
    have<-read_sas("d:/sd1/have.sas7bdat")

    mydata <- have;

    # 1. Estimate stabilized IPTW weights for multinomial treatment
    w_out <- weightit(
      TRT ~ AGE + SEX,
      data = mydata,
      method = "ps",
      estimand = "ATE",        # Average Treatment Effect in the Treated
      stabilize = TRUE,        # Stabilize weights
      verbose = FALSE
    )

    # Add weights to dataset
    mydata$WGT <- w_out$weights

    # 2. Assess covariate balance
    bal <- bal.tab(
      w_out,
      stats = c("m", "v"),     # Means and variances
      thresholds = c(m = 0.1), # Absolute SMD threshold
      disp.means = TRUE,       # Show weighted means
      un = TRUE,               # Show unweighted statistics
      pairwise = TRUE          # Compare each treatment pair
    )

    # Extract the 'balance' component and convert to data frame
    nam<-c("prop","age","sex")
    balance <- data.frame(
      nam
     ,DiffUn = bal$Balance$Diff.Un
     ,DiffADJ = bal$Balance$Diff.Adj
    )

    # Print balance assessment
    print(bal)

    # View dataset with weights
    pdf("d:/pdf/balance.pdf");
    love.plot(w_out, threshold = 0.1, binary = "std")
    summary(w_out)
    dev.off()
    fn_tosas9x(
          inp    = balance
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /* R                                                                                                                      */
    /* - Weight ranges:                                                                                                       */
    /*                                                                                                                        */
    /*            Min                                  Max                                                                    */
    /* treated 0.7730       |---------------------| 1.8927                                                                    */
    /* control 0.4385 |-------------------------|   1.8153                                                                    */
    /*                                                                                                                        */
    /* - Units with the 5 most extreme weights by group:                                                                      */
    /*                                                                                                                        */
    /*              21    119    151    172     79                                                                            */
    /*  treated 1.3703 1.4608 1.5108 1.6652 1.8927                                                                            */
    /*             129     55     69    127    103                                                                            */
    /*  control   1.62   1.62 1.7144 1.8153 1.8153                                                                            */
    /*                                                                                                                        */
    /* - Weight statistics:                                                                                                   */
    /*                                                                                                                        */
    /*         Coef of Var   MAD Entropy # Zeros                                                                              */
    /* treated       0.174 0.127   0.014       0                                                                              */
    /* control       0.381 0.303   0.068       0                                                                              */
    /*                                                                                                                        */
    /* - Effective Sample Sizes:                                                                                              */
    /*                                                                                                                        */
    /*            Control Treated                                                                                             */
    /* Unweighted   52.    148.                                                                                               */
    /* Weighted     45.52  143.66                                                                                             */
    /*                                                                                                                        */
    /* SAS  sd1.want                                                                                                          */
    /*                                                                                                                        */
    /*  NAM      DIFFUN     DIFFADJ                                                                                           */
    /*                                                                                                                        */
    /*  prop    0.57979     0.06656                                                                                           */
    /*  age     0.61502     0.16125                                                                                           */
    /*  sex     0.06445    -0.03443                                                                                           */
    /*                                                                                                                        */
    /* SAS PLOT                                                                                                               */
    /*                                                                                                                        */
    /* data ano;                                                                                                              */
    /*  set sd1.want;                                                                                                         */
    /*  ltr1=put(diffun,5.2);                                                                                                 */
    /*  ltr2=put(diffadj,5.2);                                                                                                */
    /*  ltr2=tranwrd(ltr2,'0.','.');                                                                                          */
    /*  ltr1=tranwrd(ltr1,'0.','.');                                                                                          */
    /*  diffun  = diffun -.05;                                                                                                */
    /*  diffadj = diffadj-.05;                                                                                                */
    /* run;quit;                                                                                                              */
    /*                                                                                                                        */
    /* options ls=64 ps=24;                                                                                                   */
    /* proc plot data=ano;                                                                                                    */
    /* plot nam*diffun =' ' $ ltr1                                                                                            */
    /*      nam*diffadj=' ' $ ltr2                                                                                            */
    /*         /box overlay href=-.1 0 .1;                                                                                    */
    /* run;quit;                                                                                                              */
    /*************************************************************************************************************************


    Key components explained:

    Treatment Setup:

       TRT is converted to a factor with three levels (0, 1, 2)
       focal = "1" specifies treatment level 1 as the reference group (matches SAS Treatment=1)

    Weight Estimation:

       Uses multinomial logistic regression for propensity scores
       Stabilized weights calculated as:
       $w_i = \frac{P(T_i=1)}{P(T_i=1|X_i)}$ for TRT=1
       $w_i = \frac{P(T_i=1)}{P(T_i=t|X_i)} \times \frac{P(T_i=t)}{P(T_i=1)}$ for TRT = t (t ? 1)
       Weights are normalized to improve stability

    Balance Assessment:

       Compares reference group (1) to:
       Group 0 (TRT=0 vs TRT=1)
       Group 2 (TRT=2 vs TRT=1)
       Reports for each covariate:
       Unweighted and weighted means
       Standardized mean differences (SMD)
       Variance ratios
       Sample sizes
       Highlights imbalances (absolute SMD > 0.1)

    Critical Output:

       Balance Tables: Show balance statistics for each treatment comparison
       Balance Summary: Counts of imbalanced variables
       Effective Sample Sizes: Measures weight efficiency
       Weighted Means: Primary balance assessment

     To interpret results:

       1 Check Standardized Differences (Std.Diff) - should be <0.1 after weighting
       2 Examine Variance Ratios - ideal range 0.5-2
       3 Review Effective Sample Sizes - indicates weight efficiency
       4 Look for bolded values - indicates imbalance (SMD > 0.1)

       Note: Replace the example dataset with your actual data.
       The final dataset (mydata) will contain stabilized weights
       in the WGT column matching your requested format.


       Covariance balancing, propensity scoring, and instrumental variables (IV) are related methods used
      in causal inference and observational studies to address confounding and estimate causal effects,
      but they operate differently and serve somewhat distinct purposes.

     - **Propensity Scoring**
      involves estimating the probability (propensity score) that a unit (e.g., person) receives a
      treatment given observed covariates. The goal is to balance covariates between treated and control
      groups to mimic randomized experiments, thereby reducing confounding bias in estimating treatment
      effects. Traditional propensity score methods often use logistic regression to model treatment
      assignment but can suffer if the model is misspecified.

     - **Covariate Balancing Propensity
      Scores (CBPS)** is an advanced propensity score estimation method that explicitly incorporates a
      covariate balance criterion into the estimation of the propensity score. Unlike usual propensity
      score models that focus solely on predicting treatment assignment, CBPS directly optimizes for
      balance between treatment groups while estimating the score. This approach aims to improve
      robustness to model misspecification and achieve better balance of confounders than standard
      methods[4].

     - **Instrumental Variables (IV)** are used when there is concern about unobserved
      confounding or endogeneity—situations where explanatory variables are correlated with the error
      term (e.g., due to omitted variables, reverse causality). An instrumental variable is a third
      variable correlated with the treatment but not directly with the outcome except through the
      treatment. IV methods allow identification of causal effects even when confounding cannot fully be
      controlled by observed variables alone[1][3].

     **Relations and Key Points:**

     - Both
      propensity score methods and IVs aim to reduce bias in causal effect estimation, but they do so
      differently: propensity scores balance observed covariates to emulate randomization; IVs exploit
      external variation (the instrument) to isolate exogenous changes in treatment unaffected by
      confounding[8].

     - Covariate balancing propensity scores improve upon traditional propensity
      scores by targeting covariate balance explicitly, which is crucial for valid causal inference.


     - Including an instrumental variable in propensity score modeling can be problematic: it may
      reduce "good" variation that helps identify treatment effects and increase bias, making propensity
      score methods less consistent when instruments are included as predictors[2][6].

     - In
      essence, **covariate balancing and propensity scoring are closely related**, with covariance
      balancing being a refinement in propensity score estimation, while **instrumental variables
      represent a distinct approach** to handling unobserved confounding by exploiting external variables
      that affect treatment but not directly the outcome.

     Thus, they are related causal inference
      tools with different assumptions and mechanisms for addressing confounding and endogeneity issues
      in observational data. Combining them can be complex and requires careful consideration of
      assumptions and the roles variables play in the model.

     [1]  https://www.statisticshowto.com/instrumental-variable/
     [2]  https://www.nber.org/system/files/working_papers/t0343/revisions/t0343.rev0.pdf
     [3]  https://en.wikipedia.org/wiki/Instrumental_variables_estimation
     [4]  https://pmc.ncbi.nlm.nih.gov/articles/PMC5617809/
     [5]  https://thedecisionlab.com/reference-guide/statistics/instrumental-variables-estimation
     [6]  https://ideas.repec.org/a/ebl/ecbull/eb-19-00758.html
     [7]  https://pmc.ncbi.nlm.nih.gov/articles/PMC3960904/
     [8]  https://pmc.ncbi.nlm.nih.gov/articles/PMC9271574/
     [9]  https://www.publichealth.columbia.edu/research/population-health-methods/instrumental-variables
     [10] https://www.sciencedirect.com/science/article/pii/S073510971637036X

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
