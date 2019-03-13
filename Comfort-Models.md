A comfort model is a standard definition for acceptable environmental conditions. This affects when heating and cooling systems will be activated and therefore also on how much energy a building requires in order to maintain comfortable conditions. Narrow definitions of comfort require much more mechanical work to maintain than broad definitions of comfort. 

Comfort models are also a measuring stick for evaluating the effectiveness of any given passive design strategy. 'Passive' design strategies refer to tactics which improve human comfort without mechanical systems. This might include installing a permanent shading device to block the sun, insulating the building more heavily, using a reflective window-coating to reject solar gains, or even simply opening the windows. All comfort models evaluate the impact of physiological heat flow, which is the balance of heat moving into and out of a human body. More nuanced models account for the design's impact on psychological factors that affect preferred conditions, as well as a design's ability to offer occupants control over their environment.

The tricky part is selecting the comfort model most appropriate for the design strategies you intend to test. Historically, there is a strong divide between comfort models for buildings which rely on mechanical conditioning (Predicted Mean Vote or PMV models) and buildings which are naturally ventilated (Adaptive Comfort Models). Mixed-mode buildings exist, and there are post-occupancy studies suggesting that they work well, but the literature and standards do not reflect this at as of February, 2019.

## Predicted Mean Vote (PMV) for Mechanically Conditioned Buildings

The Predicted Mean Vote (PMV) model is the only model recognized as valid for air-conditioned buildings. It is imperfect, but still the default for the HVAC industry. The model was developed by Povl Ole Fanger of Denmark in the 1970s. It is based on a physiological heat balance in the human body, and attempts to predict the average vote of a large group of people on the a seven-point thermal sensation scale where: +3 = hot, +2 = warm, +1 = slightly warm, 0 = neutral, -1 = slightly cool, -2 = cool, -3 = cold. 

This heat balance depends on many factors. Obviously, environmental conditions are important. High differences in temperature will lead to more heat gain/loss, high humidity makes it harder to cool off by sweating, and air movement accelerates heat loss/gain. Physiological heat balance also depends on our bodily makeup. For instance, some people have higher metabolisms than others, the elderly often feel colder than the young, infants are quite sensitive to any extreme, etc. 

These physiological heat flows are modeled using a combination of the following variables:
- Air temperature
- Humidity
- Air velocity
- Radiant temperature
- Clothing 
- Activity level / Metabolism of the person

Criticism of the PMV model led to the development of the Adaptive Comfort model. These criticisms included a lack of correlation between reported occupant preferences and the conditions described as comfortable by the PMV model. The model was also originally tested and developed for a test group of almost exclusively young men wearing suits, which is not representative of the global population to which it has been applied.

## Adaptive Comfort Models for Naturally Ventilated Buildings

The Adaptive Comfort models attempt to address a wider range of factors that affect human comfort. When this model was first being developed in 1997, De Dear and his team of researchers in Sydney started asking which variables are good indications of comfort? It turned out that PMV models were very poor indications of whether occupants would feel comfortable in naturally-ventilated buildings. 

![comfort model correlations](https://user-images.githubusercontent.com/44324576/52494211-b23ad180-2bcd-11e9-9845-c42387903b4c.JPG)
_The graphs above represent the amount of correlation between two variables. When there is only a weak relationship between two variables, the graph is highly random (left), and the R^2 value is closer to zero. When there is a strong relationship between the two variables (right) the graph appears as a straight line, and the R^2 value is closer to one._

Lets take a moment consider how effective PMV is as an indicator of comfort in naturally ventilated buildings. The PMV model has a relatively weak relationship to occupant's self-reported preferences for thermal comfort because it only explains 21.3% of variation among occupant comfort preference.  By comparison, air temperature _alone_ explains 23.1% of occupant responses about their preference. This means that the PMV model, in all it's nuance and complexity, is actually worse at predicting whether occupants are comfortable than a simple thermometer. **By comparison, the average outdoor air temperature over the past 30 days has an R^2 correlation with 92% of occupant responses.** This piece of evidence is a major point of departure for adaptive comfort models. Remember, however, that it has only been validated for buildings which are in entirely free-running mode, meaning there is no mechanical conditioning.

Further research into Adaptive Comfort models explored factors outside pure physiological heat balance. For example, there are nuances in our skin's way of sensing heat and air movement, which make us much more sensitive to changes in temperature than absolute temperature. Our expectations for comfort also depend upon the temperatures we have experienced over the previous days, months and years. For example, our bodies are capable of adjusting to colder temperatures in winter. Perceived comfort is also affected by the degree of control occupants have over their local environment. When occupants are able to open the windows or otherwise adjust the temperature in response to discomfort, they will accept a wider range of temperatures as comfortable.

_For more information de Dear et. al published a review article in 2013 of recent progress in research on thermal comfort, entitled Progress in Thermal Comfort Research over the last twenty years. Full citation below [2]_ 

## List of Thermal Comfort Standards
 

- **2004 - ASHRAE 55** American Society for Heating, Refrigeration and Air Conditioning Engineers, or **ASHRAE** introduces a system of two parallel comfort models for the United States, whereby **PMV** is to be used for buildings which are mechanically conditioned, and **Adaptive Comfort** is to be used for buildings which are naturally ventilated. ASHRAE 55 contains both. There is no provision for mixed-mode buildings, so these default to PMV.
- **2007 - EN 15251** - This is the standard for the EU, issued by CEN - European Committee for Standardization (Comité Européen de Normalisation). Like ASHRAE 55, it contains standards for both mechanically conditioned buildings and Adaptive Comfort. Adaptive Comfort in the EU adopts many of the same adaptive comfort concepts as ASHRAE 55, but the European Standard calculates the average outdoor temperature differently. Instead of averaging exterior temperature evenly over the previous month, it uses an exponentially weighted running mean. This means that EN 15251 places much more importance on immediately preceding days rather than an average of the entire preceding month.
- **2005 - ISO - 7730** This is an international standardization of the definition of interior comfort which is based upon a PMV model. It is not adaptive. EN 15251 actually refers to this standard as the base for PMV models of mechanical spaces.


_[1] de Dear, R. et al . (1997) Developing an adaptive model of thermal comfort and preference –
final report on RP-884 . Macquarie University, Sydney._

_[2] de Dear, Richard & Akimoto, T & Arens, Edward & Brager, Gail & Candido, Christhina & Cheong, K.W.D & Li, Baizhan & Nishihara, Naoe & Sekhar, Chandra & Tanabe, Shin-ichi & Toftum, Jorn & Zhang, H & Zhu, Yingxin. (2013). Progress in Thermal Comfort Research Over the Last Twenty Years.. Indoor Air. 23. 442-461. 10.1111/ina.12046._
