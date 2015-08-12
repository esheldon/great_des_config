# great_des_config
config files for great_des runs

metacal
--------
- sfit-degrade-e01
    - had bug not dividing sums by 4 to get mean
    - deep data run, degrading noise to that of the main
      data
- sfit-mcal-e01
    - just do max like and get metacal mean pars
    - just doing first 100 in each shear now

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
