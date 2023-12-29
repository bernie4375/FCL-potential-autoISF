


      0. Introduction                                                  readme.md in github/ bernie4375   V.2.3
             Exploring Full Closed Loop potential of-autoISF-3.0    (=        

Disclaimer – Important to read and understand 
Authors are no medical professionals but T1 diabetics (or parents of a T1D child) who report their -limited - understanding and experience, in an effort to contribute to a growing body of knowledge, and to facilitate development of patient centered solutions. 
Nothing in this site is medical advice, but meant to stimulate patient-driven self-responsible re-search, and is meant also to stimulate product developments by the medical industry. Anything you try to conclude for yourself you do on own risk. This is by no means a medical product but what is offered is a toolset for participating in development. 
Never copy what others report to use, but investigate and adjust to your data. Neglecting safety instructions, and just using the “buttons” that are made available in a supposed “learning by doing” mode, would be very dangerous with the early development stage tools this research paper is about. 
In case you choose to get deeper involved, run the system disconnected, parallel to your current glucose management, to learn its behavior before eventually considering (on own risk) to go any further. Please stay connected and share experiences, too.

Introduction.-  
Full Closed Loop using Automations is represented in AAPS Master and in the related readthedocs since autumn 2023. (https://androidaps.readthedocs.io/en/latest/Usage/FullClosedLoop.html. ).
Pre-requisites and the principal function of a Full Closed Loop, without the user ever giving a bolus and without entering any carb info are explained, also in a couple of other languages, there.
The essential points are summarized also below, in section 1.

autoISF is being developed as a much more sophisticated alternative for FCL, aiming at higher %TIR performance and/or higher degree of daily „freedom“ than simpler approaches to FCL could.
However, this demands much higher degree of involvement by the user - as you shall see, follow-ing us through this paper. Of note, parts of this paper marked in green color, notably sections 5.3 and 6.4 describing functions of the "improved FCL cockpit" are not implemented at launch because development focus had to be on more core functions. For most of these “missing elements”, work arounds are described, often involving a similarly ease to use (but requiring some extra work in your set-up) DIY FCL cockpit (see section 5.2.2.3 and 6.3 and case studies 5.2 and 6.2)

With autoISF, and especially with the intention to use it for Full Closed Loop, you are in the early development area. It is therefore important to observe the disclaimer given above, and the warnings given below, as well as the hints given by the developers in the respective manuals (readme files on their Github pages. For autoISF with AAPS the main ones are https://github.com/T-o-b-i-a-s/AndroidAPS/ and https://github.com/ga-zelle/autoISF/ ).

autoISF has also been ported into an early development branch of iAPS (oref(1) for i-Phone) (https://github.com/mountrcg/iAPS). To keep safe, please carefully observe the “readme” in github, the lack of an Automation feature and partially different nomenclature in iAPS compared to AAPS, and the very virulent discussions, notably relating to the iAPS main branch, in Discord.

First of all, a tip: If the following looks too complicated for you - and it's not just about understanding, but also about time requirements and discipline during experimentation and data analysis - you would be well advised to first try the Full Closed Loop in a simpler form with Automations (refer-ence see above, and section 13.1): Depending on the quality of their HCL tuning they are starting from, their expectations for %TIR, and on rapid carb contents of their diet, an increasing number of people succeed in making a respectable start the first time they try using AAPS in that much sim-pler Full Closed Loop mode.
See also the first published medical study that included 16 patients using AAPS, who found, on average, comparable %TIR performance when using a basic Full Closed Loop mode: https://pubmed.ncbi.nlm.nih.gov/36826996/

Alternatively you can use some techniques used in hybrid closed loop, such as using a pre-bolus with autoISF, or explore other early-DEV-variants mentioned in section 13.3, which also undergo permanent further development (Boost, AIMI, EatingNow, Tsunami).

Full Closed Loop (FCL) Using autoISF 3.0  -      v.2.3
          
0. Introduction   
1. Pre-Requisites for Full Closed Loop 
    1.1  Well tuned hybrid closed loop
    1.2  Fast insulin
    1.3 Reliable insulin delivery from pump and cannula
    1.4 Excellent CGM
    1.5 Meal-related limitations
    1.6 Lifestyle-related limitations
    1.7  Time required for setting-up
                  Case study 1.1: Occlusion   
                  Case study 1.2: Comparing insulins for FCL 
                  Case study 1.3: Jumpy CGM  
                  Case study 1.4: Lost pump connection
                  Case study 1.5: Reliable CGM values via 2 x G6
3. General Settings for Full Closed Loop  
     2.1  Range Extension (smb_max_range_extension)
     2.2  Max and Min autoISF Ratio (autoISF_min / autoISF_max)
     2.3  SMB Delivery Ratio (smb_delivery_ratio)
     2.4  iobTH (iob_threshold_percent)  
     2.5	 Eating Soon TT ?     
4. Description of autoISF 3.0 Features  
     3.1 Overview      
     3.2 ISF modulation flowcharts
     3.3 dynamic iobTH and exercise button 
     3.4 Automation options with autoISF parameters
     3.5 Activity monitor
5.  Meals: Setting ISF_weights in AAPS/Preferences  
     4.1  Getting started
     4.2  bgAccel_ISF_weight 
     4.3  pp_ISF_weight
     4.4  bgBrake_ISF_weight
     4.5  dura_ISF_weight
     4.6  Tuning initial settings
     4.7  Profile helper  
                Case study 4.1: Pizza
                Case study 4.3: Hands-off FCL on Xmas     
7.  Temp. Modulation of autoISF Aggressiveness  
     5.1  Automatic modulation of loop aggressiveness 
           5.1.1 autoISF off outside of meal windows
           5.1.2 SMB off @ odd profile target
           5.1.3 SMB off @ odd temp. target
           5.1.4 Automatic diff. of FCL aggressiveness via Automations
           5.1.5 Automatic diff. of FCL aggressiveness via Activity Monitor
           5.1.6 Pro/con completely hands-off FCL
     5.2  Manual modulation of FCL aggressiveness via DIY cockpit
           5.2.1 Status recognition
           5.2.2 Manual interventions from DIY cockpit
                5.2.2.1  Temp. %profile or TT settings
                5.2.2.2  Temp. settings in /preferences
                 5.2.2.3  Grey DIY cockpit buttons for pre-programmed FCL responses 
          5.2.3 Temporary exit from FCL
     5.3  Manual modulation of FCL aggressiveness via improved cockpit
          5.3.1  Violet FCL icon and underlying buttons 
         5.3.2  Bottom buttons “insulin” etc.
         5.3.3  Top three fields 
               5.3.3.1  TT dialogue field  
                5.3.3.2   Exercise button / dialogue field     
                5.3.3.3   Profile dialogue field   
     5.4  Recognizing loop state from the AAPS home screen
           5.4.1  Color scheme (grey/yellow) of the top 3 fields (profile, exercise, TT) 
           5.4.2  Info on the top 3 fields (profile, exercise, TT) 
           5.4.3  FCL related indicator fields
           5.4.4  Overall AAPS home screen
                  Case study 5.2: Sweet snacks / Glühwein w/ DIY cockpit
8.  Temp. Modulation for Exercise and light (In-)Activity   
       6.1  Dynamic iobTH and sensitivity ratio
            6.1.1 Manual (direct) iobTH modulation
            6.1.2 Automations for iobTH modulation
            6.1.3 Dynamic iobTH
     6.2  Temp. % profile switch
     6.3  DIY cockpit based on User action Automations
     6.4  Improved FCL cockpit  
           6.4.1 Manual (direct) iobTH modulation
           6.4.2 pre-set 4 kinds of exercise  
           6.4.3 optional meal pre-sets
           6.4.4 optional hypo management pre-sets
     6.5 Mastering the exercise after meal challenge
          6.5.1 Manual mode
          6.5.2 DIY cockpit button for User action Automation 
          6.5.3 Using pre-sets in improved FCL cockpit
     6.6  Activity monitor based on stepcounter   
                Case study 6.2 Biking day with hi carb lunch; DIY cockpit   
9. Kids: Mastering additional Challenges (fragment, to be completed NN)
10. Performance Monitoring and Tuning   
               Case study 8.2: Futility of tuning based on 1 extreme meal  
11. Trouble Shooting      
12. Emulator on PC to Determine Settings (fragment, to be completed NN)
     10.1  Logfile Analysis              
     10.2  What-if investigations
13. Emulator on the Smartphone (fragment, to be completed NN)
    11.1   AAPS home screen access to table, chart of ISF contributors for last 3 hours
    11.2   „what-if“: Real time alternative suggestions with speech synthesis)
14. Remarks for Users of previous autoISF Versions  
15. Other Avenues to Full Closed Loop
     13.1 FCL using AAPS Master and Automations
               Case study 13.1: Comparison 1 mo FCL Automation vs autoISF  
     13.2  dynamicISF used for Full Closed Loop
               Case study 13.2: Using dynISF for FCL   ( NN  )  
     13.3   Methods involving simple Meal Announcement that might be stretched into a FCL
             13.3.3.1  AIMI,   
             13.3.3.2  Boost,  
             13.3.3.3  EatNow  
             13.3.3.4  Tsunami 
     13.4  No-bolus Looping with precise Carb Inputs   
     13.5  Machine Learning (AI)  
     13.6 Dual Hormone Systems

            
