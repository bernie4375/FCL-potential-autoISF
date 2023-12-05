Exploring Full Closed Loop potential of-autoISF-3.0

Authors are no medical professionals but T1 diabetics (or parents of a T1D child) who report their -limited - understanding and experience, in an effort to contribute to a growing body of knowledge, and to facilitate development of patient centered solutions. Nothing in this site is medical advice, but meant to stimulate patient-driven self-responsible research, and meant also to stimulate and contribute to product developments by the medical industry.   

Introduction    

Full Closed Loop using Automations is represented in AAPS Master and in the related readthedocs since autumn 2023.  (https://androidaps.readthedocs.io/en/latest/Usage/FullClosedLoop.html. ).

Pre-requisites and the principal function of a Full Closed Loop, without the user ever giving a bolus and without entering any carb info are explained, also in a couple of other languages, there. 

The essential points are summarized also below, in section 1.

autoISF was developed as a much more sophisticated alternative for FCL, allowing better %TIR performance at higher degree of daily „freedom“ than simpler approaches to FCL could.  

However, this demands much higher degree of involvement by the user (as you shall see, following us through this paper).

With autoISF, and especially with the intention to use it for Full Closed Loop, you are in the early development area. It is therefore important to observe the warnings given below, as well as the hints given by the developers in the respective manuals (readme files on their Github pages; for autoISF with AAPS the main ones are https://github.com/T-o-b-i-a-s/AndroidAPS/ and https://github.com/ga-zelle/autoISF/ ).

autoISF has also been ported into an early development branch of iAPS (oref(1) for i-Phone) (https://github.com/mountrcg/iAPS).

First of all, a tip: If the following looks too complicated for you - and it's not just about understanding, but also about time requirements and discipline during implementation - you would be well advised to first try the Full Closed Loop in a simpler form with Automations (reference see above, and section 13.1):
Depending on the quality of their HCL tuning they are starting from,  their expectations for %TIR, and on rapid carb contents of their diet, an increasing number of people succeed in making a respectable start the first time they try using AAPS in Full Closed Loop mode.

See also the first published medical study that included 16 patients using AAPS, who found, on average, comparable %TIR performance when using a basic Full Closed Loop mode: https://pubmed.ncbi.nlm.nih.gov/36826996/

Alternatively - and this is also done by many people - you can use some techniques used in hybrid closed loop, such as using a pre-bolus with autoISF, or try other early DEV variants mentioned in section 13.3, which also undergo permanent further development (Boost, AIMI, EatingNow, Tsunami).


Full Closed Loop (FCL) Using autoISF 3.0   ..  V17
<- see attached files
          
1. Pre-Requisites for FCL
   1.1 Well tuned hybrid closed loop
   1.2 Fast insulin (Lyumjev, Fiasp, Apidra?)
   1.3 Good tolerance/no occlusions
   1.4 Excellent CGM
   1.5  Meal- related limitations
   1.6 Life-style related limitations
   1.7 Time required for set-up    
             Case study 1.1: Occlusion   
             Case study 1.2: Comparing insulins for FCL  
             Case study 1.3: Jumpy CGM  
             Case study 1.4: Lost pump connection  
2. General Settings for Full Closed Loop  		 
   2.1  Range Extension (smb_max_range_extension)
   2.2  Max and Min autoISF Ratio (autoISF_min / autoISF_max)
   2.3  SMB Delivery Ratio (smb_delivery_ratio)
   2.4  iobTH  (see also 3.3 and 6.1)
   2.5	Eating Soon TT    (w/ref. to „Meal Announcement “section 13)
3. Description of autoISF 3.0 features   
   3.1 Overview     
   3.2 ISF modulation flowcharts
   3.3 dynamic iobTH and exercise button 
   3.4 Automation options with autoISF parameters                                        3.5 Activity monitor
4. Meals: Setting ISF_weights in AAPS/Preferences    
   4.1  Getting started
   4.2  bgAccel_ISF_weight 
   4.3  pp_ISF_weight
   4.4  bgBrake_ISF_weight
   4.5  dura_ISF_weight
   4.6 profile helper  
             Case study 4.1: Pizza      
             Case study 4.2: Low carb meal   ( NN )
             Case study 4.3: (iAPS):   ( NN ) (example MEAL iAPS FCL)
5. Temp. Modulation of autoISF Aggressiveness   
   5.1  Automations (e.g. to manage nights )
   5.2  Cockpit use (for special situations; continued →6.2)
             Case study 5.1: Night after late fatty dinner    
             Case study 5.2 (iAPS):   ( NN ) (example iAPS FCL)
6. Temp. Modulation for Exercise and light (In-)Activity  (bernie, NN)	18
   6.1  Dynamic iobTH and sensitivity ratio         
   6.2  Managing exercise with inputs in FCL Cockpit
   6.3  Option to pre-set for 4 kinds of exercise (for 1 button operation)
   6.4 Mastering the exercise after meal challenge
   6.5 Activity monitor based on stepcounter   
            Case study 6.1: Exercise mgd. in FCL w/sports button and TT  ( NN )
            Case study 6.2 Biking day with hi carb lunch   
            Case study 6.3 (using the Activity Monitor – (ga-zelle?)
            Case study 6.4 (iAPS): (NN ) ( exercise example )
7. Kids: Mastering additional challenges (NN)    
            Case study 7.1: Active kid on med/hi carb (NN) 
            Case study 7.2: Kid on low carb ( NN )
8. Performance Monitoring and Tuning   
            Case study 8,1:    ( NN )
            Case study 8.2: Futility of tuning based on 1 extreme meal  
9. Trouble shooting      
10. Emulator on PC to Determine Settings  ( NN )                                      11. Emulator on the Smartphone  ( NN / ga-zelle? )
   11.1   Tab/table in AAPS home screen w/ table of ISF contributors  
   11.2   „what-if“ with speech synthesis
            Case study 11.1: Real-time checking out an alternative setting (NN)
12. Remarks for users of previous autoISF versions  
13. Other avenues to FCL
   13.1 FCL using AAPS Master and Automations
              Case study 13.1: Comparison 1 mo FCL Automation vs autoISF (bernie)
   13.2  dynISF used for FCL
              Case study 13.2: Using dynISF for FCL ( NN )  
   13.3  Methods involving simple Meal Announcement that might be stretched into a   .          FCL (AIMI, Boost, EatNow, Tsunami)
   13.4 How beneficial are carb entries when using oref(1) system?   
              Case study 13.3: (example - NN)
   13.5  Machine Learning (AI)  
   13.6 Dual Hormone systems


