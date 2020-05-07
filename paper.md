
Skip to content
Pull requests
Issues
Marketplace
Explore
@JosephineGigon
Learn Git and GitHub without any code!

Using the Hello World guide, you’ll start a branch, write comments, and open a pull request.
JosephineGigon /
Tests

1
0

    0

Code
Issues 0
Pull requests 0
Actions
Projects 0
Wiki
Security 0
Insights

    Settings

Tests/paper.md
@JosephineGigon JosephineGigon Add files via upload 73fd932 now
171 lines (125 sloc) 11.6 KB
title 	tags 	authors 	affiliations 	date 	bibliography
FindAge, a Python program for model ages calculation based on Pb isotopes
	
Python
	
Geology
	
Lead isotopes
	
Model ages
	
name 	orcid 	affiliation
Joséphine Gigon
	
0000-0003-0872-7098
	
1
	
name 	affiliation
Margaux Raguenel
	
2
	
name 	index
Laboratoire GeoRessources
	
1
	
name 	index
Total
	
2
	
XX May 2020
	
paper.bib
Summary

Metals are present in our everyday life and geologists try to identify their provenance. Some minerals contain clues of their history, such as galena, a lead sulphide (PbS). Lead isotopes in lead-rich minerals are one of the tools to determine the number of metal source(s) and their model age(s). FindAge is an iterative Python code that can calculate rapidly different model ages thanks to lead isotope ratios, based on the equations for different lead evolution models. In addition to be compatible with the two most used global models of lead isotope evolution, it also fit to the model developed for XXX Australia. This program is user-friendly thanks to an interface, and can be easily modified by the user for other models that could better suit the studied area. It has already been used in a scientific publication [@Gigon:2020].

#Introduction

Lead isotopes are wildly used on sulphides (galena, pyrite, pyrrhotite, sphalerite, chalcopyrite, magnetite, hematite, arsenopyrite…) and whole rock to get information about the model age of the sulphides minerals. For some minerals, this method is the only way to estimate their age. Lead isotopic ratios can be measured by TIMS (acronyme), SIMS (acronyme) or MC-ICP-MS (acronyme). One of the most used method for model age estimations is the one of Stacey:1975 which implies two stages: in the first one, the mantle evolves until 3.7 Ga, where crust formation leads to a second stage with different parameters. Another method was developed by Cumming:1975 in which a parameter increases linearly over the history of the Earth. However, this last model is not well appropriate for the Northern part of Australia and Sun:1996 modified it to better fit the Australian data. This new Python program aims to quickly calculate the model ages thanks to the Sun:1996 and Stacey:1975 models as it was designed for Proterozoic samples of the North Australian Craton. However, as the Sun:1996 model is adapted from the Cumming:1975 one only by changing one parameter value, this algorithm can be easily used for both models.

This program can be used to calculate in a short time lots of model ages and &mu values based on lead isotopes ratios. As an example, it allows the calculation of approximately 500 data in a few seconds, and with different models (two in the proposed program, and the parameters are easy to change for other similar models). The scope of this program in to calculate large sets of data when doing synthesis at regional scale for example. The
Program

The program takes as input an Excel sheet in .csv with four columns: Sample name, 206Pb/204Pb, 207Pb/204Pb and 208Pb/204Pb ratios. The output is an Excel sheet in .csv with nine columns: Sample name, calculated age with the Sun:1996 model in Ga, &mu206 (= 238U/204Pb ratio for the 206Pb decay chain in the Sun:1996 model, &mu207 (= 238U/204Pb ratio for the 207Pb decay chain in the Sun:1996 model, &Delta&mu = &mu206 - &mu207 in the Sun:1996 model, and the same parameters for the Stacey:1975 model.

Constants and unknowns

The program works with the following constants: A0 = ((206Pb)/(204Pb))t0= 9.307 [Tatsumoto:1973] B0 = ((207Pb)/(204Pb))t0= 10.294 [Tatsumoto:1973] &epsilon = 0.0833 (rate factor, Sun et al., 1996) &lambda238 = 0.155125 * 10-9 yr-1 is the decay constant of 238U &lambda235 = 0.98485 * 10-9 yr-1 is the decay constant of 235U &mup = 7.192 is the 238U/204Pb ratio of the Mantle (Tatsumoto et al., 1973) ((206Pb)/(204Pb))t is the measured 206Pb /204Pb ratio ((207Pb)/(204PbPb))t is the measured 207Pb /204Pb ratio The 1/137.88 ratio corresponds to the 235U/238U ratio, known to be constant for all U of normal isotopic composition in the Earth at the present time [Halla:2018]. The unknowns determined by the program are: t (model age of the analysed galena or sulphide) and the &mu value at that time that is found when &mu206 = &mu207, both parameters for the two proposed models.

Interface

In the interface, the user can specify several parameters that will be used in the calculation. These parameters are the emplacement of the Excelsheet containing the data, which model he wants to use if he wants the graphical representation or not. In addition, the &mu curves for different chosen values could be added to the graphical representation.

Figure 1: Interface of the FindAge program, with the different fields that have to be filled in by the user.
Lead isotopes evolution models

Cumming and Richard (1975) and Sun et al. (1996) models

The Cumming:1975 model is based on the hypothesis of a steady growth in &mu (representing the 238U/204Pb ratio of a given reservoir) through time. Based on the 206Pb/204Pb and 207Pb/204Pb, ratios, it is possible to get the model age of crystallisation of the studied mineral by iteration. In this program, the model used is the one developed by Sun:1996 for the North Australian Craton, which is the host of the mineralisation studied in this study. The equations in this model are the following ones:

$[((206Pb)/(204Pb))t=A0+&mu206[e^{4.509&lambda238}(1-&epsilon(4.509-1/&lambda238))-e^{t*&lambda238}(1-&epsilon(t-1/&lambda238))]$

$&mu206=((((206Pb)/(204Pb))t)-A0)/[e^{4.509*&lambda238}(1-&epsilon(4.509-1/&lambda238))-e^{t*&lambda238)(1-&epsilon(t-1/&lambda238))]$

and

$((207Pb)/(204 Pb))t=B0+ &mu207/137.88*[e^{4.509*&lambda235}(1-&epsilon(4.509-1/&lambda235))-e^{t*&lambd235}(1-&epsilon(t-1/&lambda235))]$

$&mu207=137.88*(((207Pb)/(204 Pb))t-B0)/[e^{4.509*&lambda235}(1-&epsilon(4.509-1/&lambda235))-e^{t*&lambda235}(1-&epsilon(t-1/&lambda235))]$

These systems are solved when &Delta&mu = &mu206-&mu207 are close to zero, and yields t and &mu206~&mu207. Cumming:1975 have chosen the rate factor &epsilon = 0.050 * 10-9 yr-1. In the Sun:1996 model, the e value has been modified, with &epsilon = 0.0833 * 10-9 yr-1 to better fit with the Australian data. This parameter can be modified in the program to calculate with one of the two models.

Stacey and Kramers (1975) model

The Stacey:1975 model implies two stages in Earth’s history: in the first one, the mantle evolves until 3.7 Ga, where crust formation leads to a second stage with different parameters. The equations in this model are the following ones:

$((206Pb)/(204Pb))t=A0+&mup*(e^{&lambda238*4.57}-e^{&lambda2383.7})+&mu206(e^{&lambda238*3.7}-e^{&lambda238*t})$

$&mu206=[((206Pb)/(204Pb))t-A0-&mup*(e^{&lambda238*4.57}-e^{&lambda2383.7})]/(e^{&lambda238*t}-e^{&lambda238*t})$

and

$((207Pb)/(204 Pb))t=B0+&mup/137.88*(e^{&lambda235*4.57}-e^{&lambda2353.7})+&mu207/137.88(e^{&lambda235*3.7}-e^{&lambda235*t})$

$&mu207=[((207Pb)/(204Pb))t-B0-&mup/137.88*(e^{&lambda235*4.57}-e^{&lambda235*3.7})]*137.88/((e^{&lambda235*3.7}-e^{&lambda235*t})$

These systems are solved when &Delta&mu = &mu206 - &mu207 are close to zero, and yields t and &mu206~&mu207.
Graphical representation

FindAge also provides a graphical representation of the analyses (black dots) as well as the isochrones for two different models '[Stacey:1975; Sun:1996]`. The isochrons defined in the program are from 0 to 3000 Ma to cover the vast majority of rocks on Earth. Figure 2 presents the results for all the lead isotopes data acquired for the XXX deposit. \autoref{fig:2}. Example of diagram provided by the FindAge program, with several isochrons (SK = Stacey and Kramers, 1975 and Sun = Sun et al., 1996). figure.\label{fig:2}
Acknowledgements

David Huston (Geoscience Australia) is thanked to have given the Excelsheet developed by AGSO-CSIRO actually used instead of this program, and to have supported this project since the beginning.
References

@article{Cumming:1975, title = {Ore lead isotope ratios in a continuously changing earth}, volume = {28}, issn = {0012821X}, url = {http://linkinghub.elsevier.com/retrieve/pii/0012821X7590223X}, doi = {10.1016/0012-821X(75)90223-X}, pages = {155--171}, number = {2}, journaltitle = {Earth and Planetary Science Letters}, author = {Cumming, G.L. and Richards, J.R.}, urldate = {2018-05-23}, date = {1975-12}, langid = {english} }

@article{Gigon:2020, title = {Tracing metal sources for the giant {McArthur} River Zn-Pb ore deposit using Pb-isotopes}, volume = {Geology}, doi = {10.1130/G47001.1}, author = {Gigon, Joséphine and Deloule, Etienne and Huston, David L. and Mercadier, Julien and Richard, Antonin and Annesley, Irvine R. and Wygralak, Andrew S. and Skirrow, Roger G. and Mernagh, T. P. and Masterman, Kristian}, date = {2020} }

@article{halla_pb_2018, title = {Pb isotopes–A multi-function tool for assessing tectonothermal events and crust-mantle recycling at late Archaean convergent margins}, volume = {320-321}, doi = {10.1016/j.lithos.2018.08.031}, pages = {207--221}, journaltitle = {Lithos}, author = {Halla, J.}, date = {2018} }

@article{Stacey:1975, title = {Approximation of terrestrial lead isotope evolution by a two-stage model}, volume = {26}, doi = {10.1016/0012-821X(75)90088-6}, pages = {207--221}, number = {2}, journaltitle = {Earth and planetary science letters}, author = {Stacey, {JS} and Kramers, {JD}}, date = {1975} }

@article{Sun:1996, title = {A continued effort to improve lead-isotope model ages}, volume = {24}, pages = {19--20}, journaltitle = {{AGSO} Research Newsletter}, author = {Sun, S. S. and Carr, G. R. and Page, R. W.}, date = {1996} }

@article{Tatsumoto:1973, title = {Time differences in the formation of meteorites as determined from the ratio of lead-207 to lead-206}, volume = {180}, doi = {10.1126/science.180.4092.1279}, pages = {1279--1283}, number = {4092}, journaltitle = {Science}, author = {Tatsumoto, Mitsunobu and Knight, Roy J. and Allegre, Claude J.}, date = {1973} }
