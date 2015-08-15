# great_des_config
config files for great_des runs

metacal
--------
- TODO

    - the TF prior is mucking up the fits a bit because it has
        a sharp feature in the flux distribution.  Need to either smooth it
        out some way or maybe just use flat but smooth priors (2-sided erf)

    - run with 3 gauss psf
        - ran the low noise version in degrade-e03
        - factor of 2 slower: limited by psf fitting

- sfit-degrade-e01
    - had bug not dividing sums by 4 to get mean
    - deep data run, degrading noise to that of the main
      data
    - checking against self
        - overall with cuts 
            [10**0.95, 10**3.0]
            [8.912509381337454, 1000.0]
            m1: -0.00246 +/- 0.0055
            m2: 0.000587 +/- 0.00607
            c1: 0.00285 +/- 0.000193
            c2: 0.00316 +/- 0.000212
    - bins of s2n_r
       s2n         m1      m1err         m2      m2err
        14    0.00162    0.00839   -0.00202    0.00725
      35.6   -0.00372    0.00578    0.00636    0.00859
        91    0.00259    0.00965   -0.00015     0.0126
       228   -0.00296     0.0156    0.00933     0.0124
       579     0.0149     0.0441     0.0509      0.026

- sfit-degrade-e02
    - B&A prior to prevent fitting problem
        m1: 0.00209 +/- 0.00704
        m2: 0.00376 +/- 0.00414
        c1: 0.00257 +/- 0.000249
        c2: 0.00298 +/- 0.000145

- sfit-degrade-e03
    - 3 gauss psf
    - B&A prior to prevent fitting problem
    - using simpler but smoother priors: multi-gauss for T based
        on actual distribution, but two-sided erf for flux

- sfit-mcal-e01
    - just do max like and get metacal mean pars

    - overall cuts only on Trat > 0.01
            m1: -0.00276 +/- 0.00077
            m2: -0.00503 +/- 0.00157
            c1: 0.0004 +/- 2.71e-05
            c2: 0.000658 +/- 5.51e-05

        s2n bins in range [8.91, 1000.0]
         s2n_r         m1      m1err         m2      m2err         c1      c1err         c2      c2err
            14   -0.00719    0.00465    -0.0106    0.00185   0.000318   0.000122    0.00101   4.91e-05
          35.6    -0.0015    0.00196   -0.00549    0.00352   0.000418   6.49e-05   0.000508   0.000116
            91  -0.000186    0.00122   -0.00348    0.00408   0.000324   4.33e-05   0.000721   0.000145
           228   -0.00352     0.0046   -0.00539    0.00602   0.000335   0.000162    0.00039   0.000211
           575   -0.00287    0.00796   3.89e-05     0.0105   0.000387   0.000283    0.00072   0.000362

        s2n bins in range [10,1000]
         s2n_r         m1      m1err         m2      m2err         c1      c1err         c2      c2err
          15.5   -0.00508    0.00349   -0.00769     0.0011   0.000303   9.47e-05   0.000887   2.99e-05
          38.6   -0.00107    0.00172   -0.00505    0.00317   0.000419   5.76e-05   0.000523   0.000107
          96.6  -0.000736    0.00168   -0.00415    0.00531   0.000336   5.95e-05   0.000662   0.000189
           236   -0.00641     0.0051   -0.00505     0.0065   0.000369   0.000188   0.000517   0.000224
           585  -0.000557    0.00847   -0.00174     0.0122   0.000447   0.000292   0.000866   0.000432

- sfit-mcal-e02
    - goes with deep run sfit-degrade-e02
    - using B&A shape prior (previous prior had issues)
    - overall with no cuts other than g < 1 and flags
        m1: 0.000935 +/- 0.00133
        m2: -0.000214 +/- 0.00132
        c1: 0.000503 +/- 0.000205
        c2: 0.0008 +/- 0.000204

    - 5 bins s2n [8.91,1000]
         s2n_r         m1      m1err         m2      m2err         c1      c1err         c2      c2err
            14  -0.000223    0.00336  -0.000215    0.00337   0.000605   0.000215    0.00127   0.000233
          35.6   -0.00119     0.0024   -0.00434    0.00239   0.000461   0.000214   0.000578   0.000211
            91  -0.000366    0.00326   -0.00399    0.00322    0.00035   0.000224   0.000718   0.000213
           228    -0.0033    0.00562   -0.00481    0.00551   0.000342   0.000275   0.000409   0.000276
           575   -0.00395     0.0112   -0.00091     0.0111   0.000373   0.000448   0.000753   0.000421

- sfit-mcal-e03
    - goes with deep run sfit-degrade-e03
    - 3 gauss psf
    - flux prior two-sided erf
    - using B&A shape prior


- sfit-noisefree-mcal-e01
    - adding some noise but not a full degrade run
- sfit-noisefree-mcal-e02
    - had bug not dividing sums by 4 to get mean
    - adding some noise but not a full degrade run
    - seem to recover the shear reasonably well
    - want to select mcal_s2n_r in the range
        [10.0**2.9,  10.0**4.0]
        794.33, 10000.0 
    - overall
        m1: 0.00185 +/- 0.00404
        m2: 0.00328 +/- 0.00276
        c1: 0.000163 +/- 0.000142
        c2: 0.000212 +/- 9.67e-05
    - vs mcal_s2n_r
    mcal_s2n_r         m1      m1err         m2      m2err
      1.02e+03    0.00236    0.00453     0.0072    0.00314
      1.68e+03  -6.59e-05    0.00386   -0.00612    0.00348
       2.8e+03    0.00727    0.00544    0.00818    0.00932
      4.63e+03    0.00853     0.0101    0.00685    0.00713
      7.67e+03    -0.0104     0.0152   -0.00668     0.0144


older
-------

m1: -0.00740639 +/- 0.00188541
m2: -0.00385091 +/- 0.00223095
c1: 7.76739e-05 +/- 6.6668e-05
c2: 1.68339e-05 +/- 7.88838e-05

m1: 0.0249632 +/- 0.00385407
m2: 0.0308756 +/- 0.00218808
c1: 0.00012853 +/- 0.000136286
c2: -5.78617e-05 +/- 7.73773e-05

New runs
    - sfit-noisefree-c01
        - error, did not use flat priors
    * sfit-noisefree-c02
        - flat priors
        - need to refit the priors from these, replace in the noisy run




- nfit-17
    - trying cosmos prior.
        - notes before run
            - efficiency is much lower, factor of two.
            - looking at the shapes I get from the noisefree runs, it seems the
              prior I have (from lackner) is also not correct, or at least does
              not match what I find.  If this run looks a bit better, we might
              try refitting the prior.
        - looks the same at high s/n
- nfit-18
    - after all the changes (norms etc., don't expect anything different)
    - don't replace cov
    - 4000 samples

- nfit-old04
    - mcmc, cosmos prior, prior *not during*, TwoSidedErf on others
    - notes before run
        - I noticed that even the noisefree ones had significantly wrong shape,
          and it turns out the sensitivity correction from nfit-02 was close to
          what was needed to correct it!  So odd.
        - So I'm rerunning with close to what I did in nfit-02, most noteworthy
          being no g prior during. If it works maybe the problem is prior
          during is just not sampling wide enough.  this would also imply that
          isample needs to be done without prior during.
        - will surprise me a bit, since the difference wasn't that big in the
          nsim runs I did, but note I only tried for high s/n and tight pdfs
    - looks bad still
    - maybe it is number of walkers?
- nfit-old05
    - same as old04 but now reverting walkers to 80, 400 burnin, 800 steps
      thin=1
    - looks about the same
    - so max is coming out 0.43, exp. value. 0.38.  max corrects to 0.05...
- nfit-old06
    - drawing guesses for walkers from prior
- nfit-old07
    - guess from gauss fit (this was in nfit-02)
    - flat priors during
    - cosmos-sersic
    - now arate looks quite similar to nfit-02

- sfit-noisefree-03
    - draw flux and priors, no prior during
    - terrible! presumably because of crazy T values that were drawn
- sfit-noisefree-04
    - random psfs
    - terrible!  That's a relief actually

# so the same trend shows up in the noisefree data.  It looks like I
# actually recover the same result in the noisy data essentially
#    so maybe focus on noisefree for a bit

- sfit-noisefree-05
    - use nm
    - bad

- sfit-noisefree-06
    - installed version of ngmix using full exp() function
    * running

- sfit-test runs
    - run with fixed version of lm without unused prior slot (on pixel was
      always zero fdiff)
        - no difference, as expected
    - ran again with new copy of data
        - looks the same

- sfit-test02
    - noisefree 004
- sfit-test03
    - noisefree 004
    - ran with more careful setting of norms in gmixes after convoluion
        - no difference
- sfit-test04
    - same as test03 but without during
    * not run yet


- do a full run on noisefree where estimate the skynoise from ~5 pixel border
    - also do this for regular images!
    - no difference

- nfit-test
    - trying broader priors and recalculating the noise
    - no different

### Checked out the old versions and got same result as nfit-02 ###

- Also checked
    - prior gives consistent answers
    - LensfitSensitivity on same samples gives same mean and sensitivity

    - generate a psf image and convolved galaxy image and fit it with both
      codes, it should give same fit
        - images are identical
        - max like fits agree
        - emcee mean of pars agree to third digit
        - sensitivities agree to 2nd digit
        - consistent with jacobian as well
        - with prior looks similar, not exact....
    - * test on meds files, outside of any framework, just write a new script
      (start with great-des or e2e)
    - * new one is 1.8 times slower... where is that coming from?
        - partly from copying psf gmix every time, no need...
        still the mcmc part is 40% slower

If error is in jacobian somehow, maybe add pixel scale to an nsim run?

T distributions

    - max like T is unimodal
    - nfit-02 is very oddly shaped
        - From that, for flat, probably want prior to extend in log(T) down to
          negative 12 or further?
    - old05 has a second population
    - nfit-16 (isample,full priors) one population but looks a bit odd
    - could this be the problem in flat runs?

- try no prior during isample?
    - is the lm cov correct?
