# Renormalization of the Random Transverse Field Ising Chain (RTFIC)

as of 5/15/18

refer to constructor for the site class. Works as a generic object with internal memory for use in lists.

Ising class:

Constructor(self, inL, inh0):

  Creates a chain of length self.L = inL of site objects with name self.system with properties:
    Jright = random number (uniform) from 0-1 to show bond strength (to the right)
    h = random number (uniform) from 0-self.h0 = inh0 to show onsite field
    ls = .5 for length of the spin
    lb = .5 for length of the bond
    m = .5 for particle spin
  creates the following storage variables:
    self.rstep = 0 is the number of renormalizations/level of renormalization
    self.Omegalist stores the (largest) energy scale at each level of renorm
    self.hlist stores each h var at each level of renorm
    self.jlist stores each Jright var at each level of renorm
    self.lslist “ “ spin cluster length “ “ “
    self. lblist “ “ bond length “ “ “
    self.mlist “ “ spin cluster magnetic moment “ “ “ 

renormalize(self):

  calls renormStep until critical condition is met (currently if ln(gamma) > 0)
  prints “failed to reach correct breakpoint” if condition is not met (before system is single site).

renormStep(self):

  preforms one renormalization (see https://journals.aps.org/prb/pdf/10.1103/PhysRevB.58.9131 for a good description)
  note: self.L is actually decremented as self.rstep contains enough information to reconstruct L

printCouplings(self):

  Gives a readable output of the current system info

printTracked(self, step = self.rstep):

  prints at inputted or current rstep:
    ave log(h)
    var log(h)
    ave log(J)
    var log(J)
    ave ls
    ave lb
    ave m
    Omega

delta(self, step = self.rstep):

  returns delta at step as mentioned in eq’n 1.8 and 1.36 of Fisher PhysRevB.51.6411 (aforementionedly referred to by just page number or eq’n number)

gamma(self, step = self.rstep):

  returns gamma at step as mentioned in eq’n 2.1

spectrumGet(self, step):

  returns the spectrum at the specified step

spectrumCompare(self):

  shows the equivalence of the two solution methods in the FFexact class.

deltaTest(self, verbose = False, startStep = 0, stopStep = self.rstep):

  prints the variance of delta over the noted levels and each delta as well if verbose

printDelta(self, stopStep = self.rstep):

  prints initial delta and delta at stopStep

gammaGraph(self, stopStep = None):

  graphs gamma over the range of first step to stopStep

lngammaGraph(self, stopStep = None):

  graphs the log of gamma over the range of first step to stopStep
  useful for finding where to chop the critical gamma

typicalLengthTest(self, verbose = False, startStep = 0, stopStep = self.rstep):

  prints the length where the typical bond length is greater than lv as defined in eq 1.31
  if verbose, then it prints each typical bond and cluster length between startStep and stopStep

typicalLengthScalingGraph(self, startStep = 0, stopStep = self.rstep):

  graphs the ratio between the typical length and gamma^2 vs step in renorm as per page 6425 before eq’n 2.100 

energyLengthScaling(self, startStep = 0, stopStep = self.rstep):

  attempts to show the relation in eq’n 1.32

typicalEnergyLengthGraph(self, startStep = 0, stopStep = self.rstep):

  attempts to show the relation in eq’n 1.33

momentPerLtest(self, startStep = 0, stopStep = self.rstep):

  attempts to show the relation between M0 and delta at the bottom of page 6437

 
 momentPerLdeltaGraph(self, startStep = 0, stopStep = self.rstep):

  graphs previous using delta as critical test

momentPerLgammaGraph(self, startStep = 0, stopStep = self.rstep):

  graphs previous using gamma as critical test
  gamma is ~ 1/abs(delta) in critical regime

typicalMomentTest(self, startStep = 0, stopStep = self.rstep):

  attempts to show eq’n 2.98

typicalMomentGammaGraph(self, startStep = 0, stopStep = self.rstep):

  graphs previous with Gamma as the scaling variable

typicalMomentDeltaGraph(self, startStep = 0, stopStep = self.rstep):

  same as above but with Delta as the scaling variable

typical2MomentGraph(self, startStep = 0, stopStep = self.rstep):

  obsolete

gapCorrLengthPlot(self, startStep = 0, stopStep = None):

  attempts to show gap correlation length correspondence but is not statistically significant on one renormalization procedure and runtime is too long to loop.

distGraph(self, startStep = 0, stopStep = self.rstep, delta = 1,  h = True, J = True, lb = False, ls = False, m = False):

  prints the log(h), log(j), ls, lb, and m lists as distributions (histograms) over the range specified for each rstep separated by delta.

FFexact Class:

  Used for solving for the spectrum via the diagonalized version of the model. Takes in and stores system size only in the constructor.


  randBuild(self, inh0):
    builds a new random system using inh0 as h0 and solves for the spectrum. Spectrum is stored in self.spectrum[]


  randBuild2(self, inh0, BC = -1):
    builds a new random system but with a (anti)periodic bountary condition set as default to anti. Solving is equivalent to randBuild if J_L happens to be zero.


  inputBuild(self, hlist, jlist):
    solves for the spectrum given the list of couplings given. Spectrum is stored in self.spectrum[]


  inputBuild2(self, hlist, jlist, BC =-1):
    same deal as randBuild2. See spectrumCompare() in the Ising class to show how these solving methods are equivalent.


  gapDistribution(self, inh0, N):
    builds N random systems with inh0 as h0 and returns the gap size between the ground state and the first excited state.


# Anderson localization for a 1-D hopping model

currently retired (4/16/18)
