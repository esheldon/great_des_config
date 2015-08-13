# great_des_config
config files for great_des runs

metacal
--------
- TODO
    - run with 3 gauss psf
        - need a degrade version and a regular metacal version

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

- sfit-mcal-e01
    - just do max like and get metacal mean pars

    - just doing first 100 in each shear now

    - overall with s2n range [10**0.95, 10**3.0] = [8.91, 1000.0]
        m1: 0.00169 +/- 0.00427
        m2: -0.0077 +/- 0.00522
        c1: 0.000355 +/- 0.000151
        c2: 0.000714 +/- 0.000183
    - in bins of s2n_r
     s2n_r         m1      m1err         m2      m2err         c1      c1err         c2      c2err
        14   0.000395     0.0116     -0.017     0.0074   0.000218   0.000296    0.00104   0.000191
      35.6    0.00732    0.00583   -0.00585     0.0102   0.000283   0.000192    0.00059   0.000338
        91    0.00482    0.00594   -0.00011    0.00689   0.000483   0.000211   0.000591   0.000239
       228    -0.0206    0.00999    -0.0107     0.0115  -0.000234   0.000367  -0.000231   0.000403
       574    -0.0182     0.0272     0.0121     0.0235  -0.000904   0.000893    0.00147   0.000752

    - adding cut on size

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
