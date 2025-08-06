***********************************************
*             ADVANCED ECONOMETRICS
*
*                Project
*
* Start Date: 23.10.2024
* Title: A Forecast Analysis: Can the UK's Labour Party Hit Their Macroeconomic Targets?
***********************************************

** Set working directory:
clear all 
cd "/Users/robmulligan/Desktop/ADV - Econometrics Project/Everything Stata

** Import Data:
use "/Users/robmulligan/Desktop/ADV - Econometrics Project/Everything Stata/FINALDATAUSE.dta"
br
drop in 213/214

** Gen a quarterly time variable ** 
gen time = qofd(Datequarterly)
format time %tq
tsset time

** Graphing to check stochastic trends/order of integration

tsline RealGDPinmillionsofpounds
tsline CPI
tsline Unemploymentrate

** Applying Transformations to make the data stationary + graphs

gen infl = (ln(CPI) - ln(L.CPI))
label variable infl "Inflation Rate (% per quarter)"
tsline infl, title("Inflation Rate 1971q1-2023q4") lcolor(red)

gen unemp = 100 * (ln(Unemploymentrate) - ln(L.Unemploymentrate))
label variable unemp "Unemployment Rate (% per quarter)"
tsline unemp, title("Unemployment Rate 1971q1-2023q4") lcolor(lime)


gen GDPGR = 100 *(ln(RealGDPinmillionsofpounds) - ln(L.RealGDPinmillionsofpounds))
label variable GDPGR "Real GDPGR (% per quarter)"
tsline GDPGR if time < tq(2020q1) | time > tq(2020q4), title("GDP Growth Rate 1971q1-2023q4") lcolor(black)

** Testing for Optimal lag length:

varsoc infl unemp GDPGR LabourPartyDummy

** ADF Tests to ensure stationarity: 

dfuller infl,lags(4) trend 
** p-value = 0 i.e., stationary
dfuller unemp,lags(4) trend
** p-value = 0 i.e., stationary
dfuller GDPGR,lags(4) trend
** p-value = 0 i.e., stationary


** Testing for cointegration (if cointegrated we must use a VEC)

vecrank RealGDPinmillionsofpounds CPI Unemploymentrate, lags(4)

*** test results say 0 integrating factors so VAR it is

** first regression
var infl GDPGR unemp LabourPartyDummy, lags(1/4) vce(robust)

** => i) Stability Checks + ii) Autocorrelation tests

*** i)

varstable, graph

		** Results
  ** All the eigenvalues lie inside the unit circle.
  ** VAR satisfies stability condition.

*** ii) 

asdoc varlmar, mlag(4) save(myLMdoc) replace



		** Results
	** There is autocorrelation at all lags

vargranger
		
		** Results
	** again, GDP and Unemploymentrate seem to cause each other
	** Neither cause inflation, and inflation does cause them


** Out of Sample Forecasts:
	
asdoc fcast compute f_, step(20) dyn(tq(2024q1)) save(my_forecast_values)

replace LabourPartyDummy = 1 if tin(2024q1, 2029q4)
	** loop in case I mess up** 
foreach var of varlist f_* {
    drop `var'
}

*** renaming variables 

label variable f_infl "Forecasted Inflation"
label variable f_infl_lb "Forecasted Inflation Lower Bound 95% CI"
label variable f_infl_ub "Forecasted Inflation Upper Bound 95% CI"

label variable f_GDPGR "Forcasted GDP Growth Rate"
label variable f_GDPGR_lb "Forcasted GDP Growth Rate Lower Bound 95% CI"
label variable f_GDPGR_ub "Forcasted GDP Growth Rate Upper Bound 95% CI"

label variable f_unemp "Forecasted Unemployment Rate"
label variable f_unemp_lb "Forecasted Unemployment Rate Lower Bound 95% CI"
label variable f_unemp_ub "Forecasted Unemployment Rate Upper Bound 95% CI"


	// Generate indicator variables for inflation being below or above 0.5%
gen below_target = f_infl < 0.5
gen above_target = f_infl >= 0.5

count if below_target == 1
count if above_target == 1

// Display the actual quarters where the condition is met
list f_infl if below_target == 1
list f_infl if above_target == 1


tsline GDPGR f_GDPGR f_GDPGR_lb f_GDPGR_ub if time < tq(2020q1) | time > tq(2020q4), ///
    legend(size(*0.6)) lpatt(solid dash dash dash) ///
	title("Forcasted GDP Growth Rate 1971q1-2029q1") ytitle("GDP Growth Rate per quarter (%)") xtitle("Time") yline(0.6)

tsline unemp f_unemp f_unemp_lb f_unemp_ub, /// 
	legend(size(*0.6)) lpatt(solid dash dash dash) /// 
	title("Unemployment Rate 1971q1-2029q1") ytitle("Unemployment Growth Rate per quarter (%)") xtitle("Time") yline(0)
	

** Outputting results:

asdoc var infl GDPGR unemp LabourPartyDummy, lags(1/4) vce(robust) save(myVARDOC) label replace title(Full Regression Results)

** Sum stats **
asdoc sum CPI RealGDPinmillionsofpounds Unemploymentrate infl GDPGR unemp f_infl f_GDPGR f_unemp, save(SUMSTATS) label replace

** assessing accuracy **

gen test = time >= tq(2015q1) // define a test sample
var GDPGR infl unemp LabourPartyDummy if test == 0, lags(1/4)
fcast compute mymodel, step(20)
gen infl_error = infl - mymodelinfl 
gen GDPGR_error = GDPGR - mymodelGDPGR
gen unemp_error = unemp - mymodelunemp

gen infl_errorsq = infl_error^2
gen GDPGR_errorsq = GDPGR_error^2
gen unemp_errorsq = unemp_error^2

egen rmse_infl = mean(infl_errorsq)
di "RMSFE for inflation:" sqrt(rmse_infl)
RMSFE for inflation:.80525491 ** when sample was 2015q1
** on average the inflation forecast is .8% off the actual value

egen rmse_GDPGR = mean(GDPGR_errorsq)
di "RMSFE for GDPGR:" sqrt(rmse_GDPGR)
RMSFE for GDPGR:.27630574 ** when sample was 2015q1
** on average the GDP forecast is .27% off the actual value

egen rmse_unemp = mean(unemp_errorsq)
di "RMSFE for unemp:" sqrt(rmse_unemp)
RMSFE for unemp:2.7656691 ** when sample was 2015q1
** on average the unemployment forecast is 2.77% off the actual value

end 
