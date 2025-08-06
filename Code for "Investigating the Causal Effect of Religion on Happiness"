****************
**             Capstone Do-File 
**         Start Date: 3/1/25
** Title: Still the Opium of the Masses: The Causal Effect of Religion on Happiness 
****************
clear all
set seed 12345
** 1) 
use "/Users/robmulligan/Desktop/CAPSTONE/Everything Stata /church_scandals.dta", clear


** 2) 
use "/Users/robmulligan/Desktop/CAPSTONE/GSS_stata 2/gss7222_r4.dta", clear

** 3)
keep year id wrkstat occ10 marital prestg10 childs age educ sex race income region partyid size polviews relig denom jew fund attend postlife pray relig16 prayer bible happy hapmar health life conclerg socfrend satjob class fear god relpersn sprtprsn relexp reliten relactiv sei10 rhhwork healthissp hlthdep weight_issp lifenow lifein5 disblty

** 4)
merge m:1 year region using "/Users/robmulligan/Desktop/CAPSTONE/Everything Stata /church_scandals.dta" 

** 5) 

gen id_new = _n
order id_new, before(id)
drop id
rename id_new id

drop D E F G H I J
drop _merge


**************
*
* Cleaning Data Section
*
**************

// Need a year var for time dummies
tab year, gen(Year)

// Need to recode the happiness variable so that it is more intuitive to work with:

recode happy (1=3) (2=2) (3=1), generate(new_happy)
label define happiness_lbl 1 "Not too happy" 2 "Pretty happy" 3 "Very happy"
label values new_happy happiness_lbl

// Need to recode the marital variable 

recode marital (1=5) (2=1) (3=2) (4=3) (5=4), gen(marital_status)
label define marital_lbl 1 "widowed" 2 "divorced" 3 "separated" 4 "single" 5 "married"
label values marital_status marital_lbl

// Need to recode the health variable
recode health (1=4) (2=3) (3=2) (4=1), gen(new_health)
label define health_lbl 1 "poor" 2 "fair" 3 "good" 4 "excellent"
label values new_health health_lbl

// Need to recode the life variable
recode life (1=3) (2=2) (3=1), gen(life_dull)
label define life_lbl 1 "dull" 2 "routine" 3 "exciting"
label values life_dull life_lbl

// Need to recode conclerg variable
recode conclerg (1=3) (2=2) (3=1), gen(trustinrelorg)
label define trustinrelorg_lbl 1 "hardly any" 2 "only some" 3 "a great deal"
label values trustinrelorg trustinrelorg_lbl 

// Need to recode socfrend variable
recode socfrend (1=7) (2=6) (3=5) (4=4) (5=3) (6=2) (7=1), gen(see_friends)
label define see_friends_lbl 1 "never" 2 "about once a year" 3 "several times a year" 4 "about once a month" 5 "several times a month" 6 "once or twice a week" 7 "almost everyday"
label values see_friends see_friends_lbl

// Need to recode satjob variable
recode satjob (1=4) (2=3) (3=2) (4=1), gen(jobsat)
label define jobsat_lbl 1 "very dissatisfied" 2 "a little dissatisfied" 3 "moderately satisfied" 4 "very satisfied"
label values jobsat jobsat_lbl

// Need to recode relpersn variable
recode relpersn (1=4) (2=3) (3=2) (4=1), gen(relperson)
label define relperson_lbl 1 "not religious at all" 2 "slightly religious" 3 "moderately religious" 4 "very religious" 
label values relperson relperson_lbl

// Need to recode sprtprsn variable 
recode sprtprsn (1=4) (2=3) (3=2) (4=1), gen(sprtperson)
label define sprtperson_lbl 1 "not spiritual at all" 2 "slightly spiritual" 3 "moderately spiritual" 4 "very spiritual" 
label values sprtperson sprtperson_lbl

// Need to recode health variable
recode health (1=4) (2=3) (3=2) (4=1), gen(healthreal)
label define healthreallbl 1 "poor" 2 "fair" 3 "good" 4 "excellent" 
label values healthreal healthreallbl

// Need to recode hlthdep variable
recode hlthdep (1=5) (2=4) (3=3) (4=2) (5=1), gen(depressed)
label define depressed_lbl 1 "very often" 2 "often" 3 "sometimes" 4 "seldom" 5 "never"
label values depressed depressed_lbl

// Need to recode postlife variable
recode postlife (1=2) (2=1) (.i=0) (.d=0) (.n=0), gen(post_life)
label define post_life_lbl 0 "don't know" 1 "no" 2 "yes"
label values post_life post_life_lbl

// Need to recode pray variable
recode pray (.i=0) (1=6) (2=5) (3=4) (4=3) (5=2) (6=1), gen(new_pray)
label define pray_lbl 0 "dont know" 1 "never" 2 "less than once a week" 3 "once a week" 4 "several times a week" 5 "once a day" 6 "several times a day"
label values new_pray pray_lbl

// Need to recode bible variable
recode bible (.i = 0) (1=4) (2=3) (3=2) (4=1), gen(bible_)
label define bible_lbl 0 "don't know" 1 "other" 2 "ancient book" 3 "inspired word" 4 "word of god"
label values bible_ bible_lbl

// Need to recode fund variable
recode fund (.i =0) (1=3) (2=2) (3=1), gen(fundamentalist)
label define fund_lbl 0 "no answer" 1 "liberal" 2 "moderate" 3 "fundamentalist"
label values fundamentalist fund_lbl

// Need to recode reliten variable
recode reliten (.i=0) (1=4) (2=3) (3=2) (4=1), gen(religious)
label define religious_lbl 0 "no answer" 1 "no religion" 2 "somewhat strong" 3 "not very strong" 4 "strong"
label values religious religious_lbl

// Need to recode relig variable
recode relig (1=1) (2=2) (3=3) (4=5) (5=5) (6=5) (7=5) (8=5) (9=4) (10=5) (11=5) (12=5) (13=5), gen(religion)
label define relig_lbl 1 "Protestant" 2 "Catholic" 3 "Jewish" 4 "Muslim" 5 "Other"
label values religion relig_lbl

// Need to recode wrkstat variable 
recode wrkstat (1=8) (2=7) (3=6) (4=1) (5=3) (6=4) (7=5) (8=2), gen(employstat)
label define emply_lbl 1 "Unemployed" 2 "Other" 3 "Retired" 4 "In School" 5 "Keeping house" 6 "With a Job but Currently not Working" 7 "Working Part Time" 8 "Working Full Time"
label values employstat emply_lbl

recode employstat (1=1) (2=2) (3=5) (4=3) (5=4) (6=6) (7=7), gen(workstat) 
label define work_lbl 1 "Unemployed" 2 "Other" 3 "In School" 4 "Keeping House" 5 "Retired" 6 "With a Job but Currently not Working" 7 "Working Part Time" 8 "Working Full Time"
label values workstat work_lbl

gen age_sq = age^2


** Relabelling all the variables to be used in the regression table

label variable religiosity "Religiosity"
label variable income "Total Household Income"
label variable educ "Education"
label variable marital_status "Marital Status"
label variable employstat "Employment Status"
label variable healthreal "Subjective Health"
label variable race "Race"
label variable sex "Sex"
label variable region "Census Division"
label variable binary_happy "Happiness"
label variable age "Age of Respondent"
label variable church_scandals "Church Scandals"
label variable workstat "Employment Status"
label variable age_sq "Age^2"




**************************
*
* Data Visualisation Section 
*
**************************
sum binary_happy religiosity church_scandals income educ marital_status workstat healthreal age_sq race sex region, detail

asdoc sum binary_happy religiosity church_scandals income educ marital_status workstat healthreal age_sq race sex region, detail label replace stats(N mean sd min max) dec(3) fhr(\b) title(Table 1: Descriptive Statistic)
estout using summary_stats.doc, cells("mean sd min max") label replace



graph bar (count) church_scandals, ///
    over(region, label(angle(45) labsize(small))) /// 
    bar(1, color(eltgreen)) ///
    ytitle("Frequency", size(small)) ///
	ylabel(,labsize(small)) ///
	scheme(stsj)
	


***
* Graphing the over-representation of Christian Religion in the Sample
***
graph bar (count), over(religion, label(angle(45))) asyvars ///
    bar(1, bcolor(gs1)) ///
    bar(2, bcolor(gs5)) ///
    bar(3, bcolor(gs8)) ///
    bar(4, bcolor(gs10)) ///
    bar(5, bcolor(gs14)) ///
    scheme(stsj) ///
    ytitle("Number of People", size(small) placement(e) margin(medium)) ///
	note("Source: General Social Survey 1972-2022", size(small)) ///
	legend(cols(5) size(small)) ylabel(, labsize(small))
	
	
graph bar (count), over(religion, label(angle(45))) asyvars ///
    bar(1, bcolor("eltblue")) /// Light Blue
    bar(2, bcolor("lblue"))   /// Sky Blue
    bar(3, bcolor("ebblue"))    /// Medium Blue
    bar(4, bcolor("blue"))  ///
    bar(5, bcolor("purple"))  ///
    scheme(stsj) ///
    ytitle("Number of People", size(small) placement(e) margin(medium)) ///
    legend(cols(5) size(small)) ylabel(, labsize(small))

	
	
	
	
	
	
***
* Graphing the differences in trust in religious organisations between regions 
***
	
// Filter data for South Atlantic and Middle Atlantic regions
gen region_filter = (region == 2 | region == 6)

gen trust_hardly = trustinrelorg == 1
gen trust_some = trustinrelorg == 2
gen trust_great = trustinrelorg == 3

label variable trust_hardly "Low Trust"
label variable trust_some "Some Trust"
label variable trust_great "A Lot of Trust"

** Graph showing difference in trust between the highest and lowest church scandal rates

graph bar (sum) trust_hardly trust_some trust_great if region_filter == 1, ///
    over(region) ///
    bar(1, color(blue)) bar(2, color(red)) bar(3, color(green)) ///
    title("Frequency of Trust Levels in Religious Organizations by Region", size(medium)) ///
    ytitle("Frequency", size(medium)) ///
	scheme(stsj)
    
** Graph showing difference in trust between all regions

graph bar (sum) trust_hardly trust_some trust_great, ///
    over(region, label(angle(45) labsize(small))) /// 
    bar(1, color(gs2)) bar(2, color(gs5)) bar(3, color(gs8)) ///
    ytitle("Frequency", size(small) margin(medium)) ///
	ylabel(, labsize(small)) ///
	legend(order(1 "Hardly Any Trust" 2 "Some Trust" 3 "A Lot of Trust") cols(3) size(small)) ///
	scheme(stsj) 
	
		
	
	

graph bar (sum) trust_hardly trust_some trust_great, ///
    over(region, label(angle(45) labsize(small))) /// 
    bar(1, color(ebblue)) bar(2, color(eltblue)) bar(3, color(blue)) ///
    ytitle("Frequency", size(small) margin(medium)) ///
	ylabel(, labsize(small)) ///
	legend(order(1 "Hardly Any Trust" 2 "Some Trust" 3 "A Lot of Trust") cols(3) size(small)) ///
	scheme(stsj) 

	
	

** Graph showing difference in trust between all regions WITH church scandal line

twoway (bar trust_hardly region, barwidth(0.8) color(blue)) ///
       (bar trust_some region, barwidth(0.8) color(red)) ///
       (bar trust_great region, barwidth(0.8) color(green)) ///
       (line churchscandal region, lcolor(black) lwidth(medium)), ///
    xlabel(, angle(90) labsize(small)) ///
    ylabel(, labsize(small)) ///
    title("Trust in Religious Organizations and Church Scandals by Region", size(medium)) ///
    ytitle("Frequency", size(medium)) ///
    legend(order(1 "Hardly" 2 "Some" 3 "Great" 4 "Church Scandals")) ///
    scheme(sj)

** Graph showing men and woman are differing levels of religious
gen male = sex == 1
gen female = sex == 2


graph bar (sum) male female, /// 
	over(attend, label(angle(45) labsize(vsmall))) ///
	bar(1, color(gs3)) bar(2, color(gs6)) ///
	ytitle("Frequency", size(small)) ///
	note("Source: General Social Survey 1972-2022", size(vsmall)) /// 
	legend(order(1 "Male" 2 "Female"))
	scheme(stsj)
	
	
	
graph bar (sum) male female, /// 
	over(attend, label(angle(45) labsize(vsmall))) ///
	bar(1, color(blue)) bar(2, color(pink)) ///
	ytitle("Frequency", size(small)) ///
	legend(order(1 "Male" 2 "Female")) ///
	scheme(stsj)
	
	
** same as above just with happiness scores

graph bar (sum) male female, /// 
	over(new_happy, label(angle(90) labsize(small))) ///
	bar(1, color(ltblue)) bar(2, color(pink)) ///
	title("Men and Woman Differing Levels of Happiness") ///
	ytitle("Frequency", size(small)) ///
	scheme(sj)


** Graph showing blacks and whites are differing levels of religious
gen white = race == 1
gen black = race == 2
	** need to weight the frequencies so as to not skew the graph
drop race_weight
gen race_weight = cond(race == 2, 57, 10)

graph bar (sum) white black [fw=race_weight], ///
    over(attend, label(angle(45) labsize(small))) ///
    bar(1, color(gs3)) bar(2, color(gs6)) ///
    ytitle("Weighted Frequency", size(small)) ///
	note("Source: General Social Survey 1972-2022", size(vsmall)) /// 
	legend(order(1 "White" 2 "Black"))
    scheme(stsj)

graph bar (sum) white black [fw=race_weight], ///
    over(attend, label(angle(45) labsize(small))) ///
    bar(1, color(blue)) bar(2, color(pink)) ///
    ytitle("Weighted Frequency", size(small)) ///
	legend(order(1 "White" 2 "Black")) ///
    scheme(stsj)	
	
	
	

** same as above just with happy

graph bar (sum) white black [fw=race_weight], ///
    over(new_happy, label(angle(90) labsize(small))) ///
    bar(1, color(magenta)) bar(2, color(midblue)) ///
    title("Happiness Differences in Race (Weighted)") ///
    ytitle("Weighted Frequency", size(small)) ///
    scheme(sj)


** graph showing age differences in religious
gen young = age <= 44
gen old = age >= 44

graph bar (sum) young old, ///
	over(attend, label(angle(90) labsize(small))) ///
	bar(1, color(ebblue)) bar(2, color(edkblue)) ///
	title("Religious Differences in Age") ///
	ytitle("Frequency", size(small)) ///
	scheme(sj)

** same as above just with happy

graph bar (sum) young old, ///
	over(new_happy, label(angle(90) labsize(small))) ///
	bar(1, color(ebblue)) bar(2, color(edkblue)) ///
	title("Happiness Differences in Age") ///
	ytitle("Frequency", size(small)) ///
	scheme(sj)

** showing the trend in not too happy + decrease in religious attend
gen not_happy = new_happy == 1
gen new_variable = new_happy == 2
gen very_happy = new_happy == 3
gen not_attend = attend == 0


twoway scatter not_happy year if not_happy == 1
///
	   (scatter not_attend year)


graph bar (sum) not_happy, ///
	over(year, label(angle(90) labsize(small))) ///
	bar(1, color(purple)) ///
	title("Trending Unhappiness") ///
	ytitle("Frequency", size(samll)) ///
	scheme(sj)

graph bar (sum) new_variable, ///
	over(year, label(angle(90) labsize(small))) ///
	bar(1, color(blue)) ///
	title("Trending baseline happiness") ///
	ytitle("Frequency", size(samll)) ///
	scheme(sj)
	
graph bar (sum) very_happy, ///
	over(year, label(angle(90) labsize(small))) ///
	bar(1, color(blue)) ///
	title("Trending baseline happiness") ///
	ytitle("Frequency", size(samll)) ///
	scheme(sj)
	
	
graph bar (sum) not_attend, ///
	over(year, label(angle(90) labsize(small))) ///
	bar(1, color(purple)) ///
	title("Trend in Not Attending") ///
	ytitle("Frequency", size(samll)) ///
	scheme(sj)

tabstat attend new_pray post_life bible_ trustinrelorg relig16 religious fundamentalist, stat(n mean) save
return list
	
	
reg religiosity age age_sq 
	
reg religiosity age age_sq, robust
margins, at(age=(18(2)90)) // Predict values from age 18 to 90
marginsplot, title("") ///
    xtitle("Age") ytitle("Predicted Religiosity") ///
    plotopts(lwidth(medium) color(blue)) ///
	scheme(stsj)

twoway scatter not_happy year

graph bar (count) not_happy, ///
over(year, label(angle(90) labsize(small))) ////
title("Increase in Unhappiness Overtime") ///
ytitle("Frequency", size(small))
scheme(sj)

tab year if not_happy > 0








preserve
collapse (count) not_happy, by(year) // Summarize counts per year
twoway (bar not_happy year, barwidth(0.8) color(blue)) ///
       (lfit not_happy year, lcolor(red)), ///
       ytitle("Frequency", size(small)) ///
       xtitle("Year") ///
       xlabel(1970(2)2024, angle(90) labsize(small)) /// Adjust range as needed
       legend(order(1 "Unhappiness" 2 "Fitted Line")) ///
       scheme(stsj)

restore

preserve
collapse (count) not_happy, by(year) // Summarize counts per year
levelsof year if not_happy > 0, local(years)
twoway (bar not_happy year, barwidth(0.8) color(blue)) ///
       (lfit not_happy year, lcolor(red)), ///
       title("Increase in Unhappiness Over Time") ///
       ytitle("Frequency", size(small)) ///
       xtitle("Year") ///
       xlabel(`years', angle(90) labsize(small)) /// Auto-generates labels
       legend(order(1 "Unhappiness" 2 "Fitted Line")) ///
       scheme(sj)
restore  

preserve
collapse (count) not_attend, by(year) // Summarize counts per year
twoway (bar not_attend year, barwidth(0.8) color(ebblue)) ///
       (lfit not_attend year, lcolor(red)), ///
       ytitle("Frequency", size(small)) ///
       xtitle("Year") ///
       xlabel(1970(2)2024, angle(90) labsize(small)) /// Adjust range as needed
       legend(order(1 "No Attendance" 2 "Fitted Line")) ///
       scheme(stsj)

restore







gen not_attend = 1 if attend == 0
gen not_happy = 1 if new_happy == 1


	
	
*******************************
*                             *
* Empirical Approach Section  *
*                             *
*******************************


** step 1) Factor Analysis 

// Variables to be included: attend new_pray post_life bible_ trustinrelorg relig16 religious fundamentalist 

preserve
polychoric attend new_pray post_life bible_ trustinrelorg relig16 religious fundamentalist 
restore

matrix mypoly = r(R)
factormat mypoly, n(72390) ml
predict factor1
rotate, promax
rename factor1 religiosity
estat kmo


** Step 2) LPM
*** Step 2.1) split ordinal happy into binary happy:
**** this is putting only "very happy" people as happy and everyone else as not happy

gen binary_happy =.
replace binary_happy = 1 if new_happy == 3
replace binary_happy = 0 if new_happy == 1 | 2

*** Step 2.2) IV Regressions + output nice little table

ivreg2 binary_happy (religiosity=church_scandals) Year1-Year34, robust first savefirst
estimates store my_results_reg1
outreg2 my_results_reg1 using myreg1.doc, word replace title(Does Religion Affect Happiness) addtext(Time Dummies Included, YES, Controls Included, NO, Estimation Method, LPM) label drop(Year1-Year34 region) dec(3) 
est restore _ivreg2_religiosity
outreg2 _ivreg2_religiosity using myIVresults.doc, replace title(First Stage Results) addtext(Time Dummies Included, NO, Controls Included, NO, Estimation Method, OLS) label dec(4) drop(Year1-Year34 region)


** in latex **

ivreg2 binary_happy (religiosity=church_scandals) Year1-Year34, robust first savefirst
estimates store my_results_reg1
outreg2 my_results_reg1 using myreg1, tex replace title(Does Religion Affect Happiness) addtext(Time Dummies Included, YES, Controls Included, NO, Estimation Method, LPM) label drop(Year1-Year34 region) dec(3) 







ivreg2 binary_happy income educ workstat marital_status Year1-Year34 (religiosity=church_scandals), robust first savefirst
estimates store my_results_reg2
outreg2 my_results_reg2 using myreg1.doc, word append title(Does Religion Affect Happiness) addtext(Time Dummies Included, YES, Controls Included, NO, Estimation Method, LPM) label drop(Year1-Year34 region) dec(3) sortvar(religiosity income educ employstat marital_status)
est restore _ivreg2_religiosity
outreg2 _ivreg2_religiosity using myIVresults.doc, append title(First Stage Results) addtext(Time Dummies Included, NO, Controls Included, NO, Estimation Method, OLS) label dec(4) drop(Year1-Year34 region) sortvar(church_scandals income educ workstat marital_status)


ivreg2 binary_happy income educ age_sq healthreal race sex region marital_status workstat Year1-Year34 (religiosity=church_scandals), robust first savefirst
estimates store my_results_reg4
outreg2 my_results_stage1 using myreg1.doc, word append title(Does Religion Affect Happiness)  addtext(Time Dummies Included, YES, Controls Included, YES, Estimation Method, LPM) label drop(Year1-Year34 region race sex region) dec(3) sortvar(religiosity income educ workstat marital_status age_sq healthreal)
est restore _ivreg2_religiosity
outreg2 _ivreg2_religiosity using myIVresults.doc, append title(First Stage Results) addtext(Time Dummies Included, YES, Controls Included, YES, Estimation Method, OLS) label dec(4) drop(Year1-Year34 region race sex region) sortvar(church_scandals income educ workstat marital_status age healthreal)


** Step 2.3 Normal OLS regressions for comparisons sake

reg binary_happy religiosity Year1-Year34, robust 
estimates store my_OLSresults_reg1
outreg2 my_OLSresults_reg1 using myolsreg.doc, word replace title (Does Religion Affect Happiness: OLS results) addtext(Time Dummies Included, NO, Controls Included, NO, Estimation Method, OLS) label drop(Year1-Year34 region) dec(3)

reg binary_happy religiosity income educ workstat marital_status Year1-Year34, robust
estimates store my_OLSresults_reg2 
outreg2 my_OLSresults_reg2 using myolsreg.doc, word append addtext(Time Dummies Included, YES, Controls Included, NO, Estimation Method, OLS) label drop(Year1-Year34 region) dec(3) sortvar(religiosity income educ employstat marital_status) 

reg binary_happy religiosity income educ age_sq healthreal race sex region marital_status workstat Year1-Year34, robust
estimates store my_OLSresults_reg3
outreg2 my_OLSresults_reg3 using myolsreg.doc, word append addtext(Time Dummies Included, YES, Controls Included, YES, Estimation Method, OLS) label drop(Year1-Year34 region race sex region) dec(3) sortvar(religiosity income educ workstat marital_status age_sq healthreal) 

** exporting:
outreg2 my_OLSresults_reg1 my_OLSresults_reg2 my_OLSresults_reg3 using mymerged.doc, word replace title(Does Religion Affect Happiness) addtext(Time Dummies Included, NO, Controls Included, NO, Estimation Method, OLS) label drop(Year1-Year34 region) dec(3)
outreg2 my_results_reg1 my_results_reg2 my_results_reg4 using mymerged.doc, word append title(Does Religion Affect Happiness) addtext(Time Dummies Included, NO, Controls Included, NO, Estimation Method, LPM) label drop(Year1-Year34 region) dec(3)




** spare regressions
** ivreg2 binary_happy income educ workstat marital_status race sex age_sq region healthreal (religiosity=church_scandals), robust first savefirst
** estimates store my_results_reg3
** outreg2 my_results_reg3 using myreg.doc, word append title(Does Religion Affect Happiness) ctitle(Model 3) addtext(Time Dummies Included, NO, Controls Included, YES, Estimation Method, LPM) label drop(Year1-Year34 race sex region) dec(3) sortvar(religiosity income educ workstat marital_status healthreal)
** est restore _ivreg2_religiosity
** outreg2 _ivreg2_religiosity using myIVresults.doc, append title(First Stage Results) ctitle(Model 3) addtext(Time Dummies Included, NO, Controls Included, YES, Estimation Method, OLS) label dec(4) drop(Year1-Year34 region race sex region) sortvar(church_scandals income educ workstat marital_status healthreal) 




mvtest normality attend new_pray post_life bible_ trustinrelorg relig16 religious fundamentalist, mardia



egen md = md(attend new_pray post_life bible_ trustinrelorg relig16 religious fundamentalist), cov


















return list
display "Kleibergen-Paap F-stat: " e(widstat)
display "Stock-Yogo Critical Values: " e(systest)
local kp_fstat = e(widstat)
local cd_fstat = e(cdstat)

matrix results = (`kp_fstat', `cd_fstat')
matrix list results



*** Step 2.3) Exporting Regression
estimates store my_results_stage1
outreg2 my_results_stage1 using myreg.doc, word replace title(Does Religion Affect Happiness) ctitle(Happiness) addtext(Time Dummies Included, YES, Controls Included, YES, Estimation Method, LPM) label drop(Year1-Year34 region) dec(3)




tabstat attend, stat(n mean)
tabstat new_pray, stat(n mean)
tabstat post_life, stat(n mean)
tabstat bible_, stat(n mean)
tabstat trustinrelorg, stat(n mean)
tabstat relig16, stat(n mean)
tabstat religious, stat(n mean)
tabstat fundamentalist, stat(n mean)


reg workstat religiosity, robust
reg religiosity workstat, robust





** messing around **

reg binary_happy religiosity income educ age_sq healthreal race sex region marital_status workstat Year1-Year34, robust
estimates store OLS_model




ivreg2 binary_happy income educ age_sq healthreal race sex region marital_status workstat Year1-Year34 (religiosity=church_scandals), robust 
estimates store IV_Model

* Simplified coefplot
coefplot OLS_model IV_Model, ///
    keep(religiosity) ///
    vertical ///
    recast(bar) ///
    barwidth(0.3) ///
    ciopts(recast(rcap)) ///
    title("Comparison of OLS and IV Estimates") ///
    subtitle("Religiosity Coefficient") ///
    ytitle("Coefficient Size") ///
    legend(label(1 "OLS") label(2 "IV")) ///
    xlabel(, noticks) ///
    plotregion(color(white)) ///
    graphregion(color(white))

coefplot ols iv, keep(religiosity) xline(0) vertical recast(bar) barwidth(0.2) ciopts(recast(rcap)) title("Comparison of OLS and IV Estimates") subtitle("Religiosity Coefficient") ytitle("Coefficient Size") legend(label(1 "OLS") label(2 "IV"))



coefplot OLS_model IV_Model, ///
    keep(religiosity) ///
    rename(OLS_model = "OLS" IV_Model = "IV") ///
    vertical ///
    title("Comparison of OLS and IV Estimates") ///
    subtitle("Religiosity Coefficient") ///
    ytitle("Coefficient Size") ///
    legend(off) ///
    xlabel(, noticks)












preserve
* Step 2: Create a clean dataset using scalars
clear
set obs 2
gen str10 model = ""
gen coef = .
gen lb = .
gen ub = .

replace model = "OLS" in 1
replace coef = ols_coef in 1
replace lb = ols_lb in 1
replace ub = ols_ub in 1

replace model = "IV" in 2
replace coef = iv_coef in 2
replace lb = iv_lb in 2
replace ub = iv_ub in 2

gen model_num = .
replace model_num = 1 if model == "OLS"
replace model_num = 2 if model == "IV"

* Step 2: Plot using numeric identifiers
twoway (bar coef model_num, barwidth(0.4)) ///
       (rcap lb ub model_num, lcolor(black)), ///
       xlabel(1 "OLS" 2 "IV", noticks) ///
       ytitle("Coefficient Size") ///
       title("Comparison of OLS and IV Estimates") ///
       subtitle("Religiosity Coefficient") ///
       legend(off) ///
       xtitle("") // Remove default x-axis title

restore

















