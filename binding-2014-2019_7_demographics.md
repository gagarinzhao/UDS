Binding Selected CQM Table 7 Demographics 2014-2019
================
Gagarin Zhao
8/27/2020

Export years 2014-2019 joined as XLSX. Following years can be added as
time goes on.

``` r
uds2014to2019.t7 = bind_rows(uds2014info.t7, uds2015info.t7, uds2016info.t7, uds2017info.t7, uds2018info.t7, uds2019info.t7)
```

    ## Error in list2(...): object 'uds2014info.t7' not found

Selecting only TOTAL rows, ignoring race/ethnicity for now, renaming for
easier usage in PowerBI. Other variables can be quickly added here.

``` r
uds2014to2019.t7_demographics = uds2014to2019.t7 %>% 
  select(HealthCenterName,
         BHCMISID,
         ReportingYear,
         A_HIV_pos_preg_women = T7_L0_C0, #section A - deliveries and birth weight
         A_deliveries_performed = T7_L2_C0,
         A_total_deliveries = T7_Li_C1a,
         A_total_live_births_below_1500g = T7_Li_C1b,
         A_total_live_births_1500_2499g = T7_Li_C1c,
         A_total_live_births_above_2500g = T7_Li_C1d,
         #hispanic/latino + non h/l subtotals
         A_subtotal_deliveries_HL = T7_LSTHL_C1a,
         A_subtotal_live_births_below_1500g_HL = T7_LSTHL_C1b,
         A_subtotal_live_births_1500_2499g_HL = T7_LSTHL_C1c,
         A_subtotal_live_births_above_2500g_HL = T7_LSTHL_C1d,
         A_subtotal_deliveries_NHL = T7_LSTNHL_C1a,
         A_subtotal_live_births_below_1500g_NHL = T7_LSTNHL_C1b,
         A_subtotal_live_births_1500_2499g_NHL = T7_LSTNHL_C1c,
         A_subtotal_live_births_above_2500g_NHL = T7_LSTNHL_C1d,
         
         #first column
         A_deliveries_HL_asian = T7_L1a_C1a,
         A_deliveries_HL_nativehawaiian = T7_L1b1_C1a,
         A_deliveries_HL_otherpacificislander = T7_L1b2_C1a,
         A_deliveries_HL_blackAA = T7_L1c_C1a,
         A_deliveries_HL_indianAN = T7_L1d_C1a,
         A_deliveries_HL_white = T7_L1e_C1a,
         A_deliveries_HL_morethanone = T7_L1f_C1a,
         A_deliveries_HL_unreported = T7_L1g_C1a,
         
         A_deliveries_NHL_asian = T7_L2a_C1a,
         A_deliveries_NHL_nativehawaiian = T7_L2b1_C1a,
         A_deliveries_NHL_otherpacificislander = T7_L2b2_C1a,
         A_deliveries_NHL_blackAA = T7_L2c_C1a,
         A_deliveries_NHL_indianAN = T7_L2d_C1a,
         A_deliveries_NHL_white = T7_L2e_C1a,
         A_deliveries_NHL_morethanone = T7_L2f_C1a,
         A_deliveries_NHL_unreported = T7_L2g_C1a,
         
         A_deliveries_refused_race_eth = T7_Lh_C1a,
         
         #second column
         A_live_births_below_1500g_HL_asian = T7_L1a_C1b,
         A_live_births_below_1500g_HL_nativehawaiian = T7_L1b1_C1b,
         A_live_births_below_1500g_HL_otherpacificislander = T7_L1b2_C1b,
         A_live_births_below_1500g_HL_blackAA = T7_L1c_C1b,
         A_live_births_below_1500g_HL_indianAN = T7_L1d_C1b,
         A_live_births_below_1500g_HL_white = T7_L1e_C1b,
         A_live_births_below_1500g_HL_morethanone = T7_L1f_C1b,
         A_live_births_below_1500g_HL_unreported = T7_L1g_C1b,

         A_live_births_below_1500g_NHL_asian = T7_L2a_C1b,
         A_live_births_below_1500g_NHL_nativehawaiian = T7_L2b1_C1b,
         A_live_births_below_1500g_NHL_otherpacificislander = T7_L2b2_C1b,
         A_live_births_below_1500g_NHL_blackAA = T7_L2c_C1b,
         A_live_births_below_1500g_NHL_indianAN = T7_L2d_C1b,
         A_live_births_below_1500g_NHL_white = T7_L2e_C1b,
         A_live_births_below_1500g_NHL_morethanone = T7_L2f_C1b,
         A_live_births_below_1500g_NHL_unreported = T7_L2g_C1b,

         A_live_births_below_1500g_refused_race_eth = T7_Lh_C1b,
         
         # third column
         A_live_births_1500_2499g_HL_asian = T7_L1a_C1c,
         A_live_births_1500_2499g_HL_nativehawaiian = T7_L1b1_C1c,
         A_live_births_1500_2499g_HL_otherpacificislander = T7_L1b2_C1c,
         A_live_births_1500_2499g_HL_blackAA = T7_L1c_C1c,
         A_live_births_1500_2499g_HL_indianAN = T7_L1d_C1c,
         A_live_births_1500_2499g_HL_white = T7_L1e_C1c,
         A_live_births_1500_2499g_HL_morethanone = T7_L1f_C1c,
         A_live_births_1500_2499g_HL_unreported = T7_L1g_C1c,
         
         
         A_live_births_1500_2499g_NHL_asian = T7_L2a_C1c,
         A_live_births_1500_2499g_NHL_nativehawaiian = T7_L2b1_C1c,
         A_live_births_1500_2499g_NHL_otherpacificislander = T7_L2b2_C1c,
         A_live_births_1500_2499g_NHL_blackAA = T7_L2c_C1c,
         A_live_births_1500_2499g_NHL_indianAN = T7_L2d_C1c,
         A_live_births_1500_2499g_NHL_white = T7_L2e_C1c,
         A_live_births_1500_2499g_NHL_morethanone = T7_L2f_C1c,
         A_live_births_1500_2499g_NHL_unreported = T7_L2g_C1c,         
         
         A_live_births_1500_2499g_refused_race_eth = T7_Lh_C1c,
         
         #fourth column
         A_live_births_above_2500g_HL_asian = T7_L1a_C1d,
         A_live_births_above_2500g_HL_nativehawaiian = T7_L1b1_C1d,
         A_live_births_above_2500g_HL_otherpacificislander = T7_L1b2_C1d,
         A_live_births_above_2500g_HL_blackAA = T7_L1c_C1d,
         A_live_births_above_2500g_HL_indianAN = T7_L1d_C1d,
         A_live_births_above_2500g_HL_white = T7_L1e_C1d,
         A_live_births_above_2500g_HL_morethanone = T7_L1f_C1d,
         A_live_births_above_2500g_HL_unreported = T7_L1g_C1d,
         
         
         A_live_births_above_2500g_NHL_asian = T7_L2a_C1d,
         A_live_births_above_2500g_NHL_nativehawaiian = T7_L2b1_C1d,
         A_live_births_above_2500g_NHL_otherpacificislander = T7_L2b2_C1d,
         A_live_births_above_2500g_NHL_blackAA = T7_L2c_C1d,
         A_live_births_above_2500g_NHL_indianAN = T7_L2d_C1d,
         A_live_births_above_2500g_NHL_white = T7_L2e_C1d,
         A_live_births_above_2500g_NHL_morethanone = T7_L2f_C1d,
         A_live_births_above_2500g_NHL_unreported = T7_L2g_C1d,         
         
         A_live_births_above_2500g_refused_race_eth = T7_Lh_C1d,         
         
         
         ####section B - high blood pressure
         B_total_pat_hypertension_18_85 = T7_Li_C2a,
         B_total_num_charts_samp_hypertension = T7_Li_C2b,
         B_total_pat_hypertension_controlled = T7_Li_C2c,
         #hispanic/latino + non h/l subtotals
         B_subtotal_pat_hypertension_18_85_HL = T7_LSTHL_C2a,
         B_subtotal_num_charts_samp_hypertension_HL = T7_LSTHL_C2b,
         B_subtotal_pat_hypertention_controlled_HL = T7_LSTHL_C2c,
         B_subtotal_pat_hypertension_18_85_NHL = T7_LSTNHL_C2a,
         B_subtotal_num_charts_samp_hypertension_NHL = T7_LSTNHL_C2b,
         B_subtotal_pat_hypertention_controlled_NHL = T7_LSTNHL_C2c,
         
         #asian HL
         B_pat_hypertension_18_85_HL_asian = T7_L1a_C2a,
         B_num_charts_samp_hypertension_HL_asian = T7_L1a_C2b,
         B_pat_hypertension_controlled_HL_asian = T7_L1a_C2c,         
         
         #Native Hawaiian HL
         B_pat_hypertension_18_85_HL_nativehawaiian = T7_L1b1_C2a,
         B_num_charts_samp_hypertension_HL_nativehawaiian = T7_L1b1_C2b,         
         B_pat_hypertension_controlled_HL_nativehawaiian = T7_L1b1_C2c,         
         
         #other pacific islander HL
         B_pat_hypertension_18_85_HL_otherpacificislander = T7_L1b2_C2a,
         B_num_charts_samp_hypertension_HL_otherpacificislander = T7_L1b2_C2b,
         B_pat_hypertension_controlled_HL_otherpacificislander = T7_L1b2_C2c,
         
         #black / african american HL
         B_pat_hypertension_18_85_HL_blackAA = T7_L1c_C2a,
         B_num_charts_samp_hypertension_HL_blackAA = T7_L1c_C2b,
         B_pat_hypertension_controlled_HL_blackAA = T7_L1c_C2c,
         
         #american indian / alaskan native HL
         B_pat_hypertension_18_85_HL_indianAN = T7_L1d_C2a,
         B_num_charts_samp_hypertension_HL_indianAN = T7_L1d_C2b,
         B_pat_hypertension_controlled_HL_indianAN = T7_L1d_C2c,         
         
         #white HL
         B_pat_hypertension_18_85_HL_white = T7_L1e_C2a,
         B_num_charts_samp_hypertension_HL_white = T7_L1e_C2b,         
         B_pat_hypertension_controlled_HL_white = T7_L1e_C2c,
         
         #more than one race HL
         B_pat_hypertension_18_85_HL_morethanone = T7_L1f_C2a,
         B_num_charts_samp_hypertension_HL_morethanone = T7_L1f_C2b,
         B_pat_hypertension_controlled_HL_morethanone = T7_L1f_C2c,
         
         #unreported HL
         B_pat_hypertension_18_85_HL_unreported = T7_L1g_C2a,
         B_num_charts_samp_hypertension_HL_unreported = T7_L1g_C2b,  
         B_pat_hypertension_controlled_HL_unreported = T7_L1g_C2c,         
         
         #asian NHL
         B_pat_hypertension_18_85_NHL_asian = T7_L2a_C2a,
         B_num_charts_samp_hypertension_NHL_asian = T7_L2a_C2b,  
         B_pat_hypertension_controlled_NHL_asian = T7_L2a_C2c,
         
         #native hawaiian NHL
         B_pat_hypertension_18_85_NHL_nativehawaiian = T7_L2b1_C2a,
         B_num_charts_samp_hypertension_NHL_nativehawaiian = T7_L2b1_C2b,
         B_pat_hypertension_controlled_NHL_nativehawaiian = T7_L2b1_C2c,         
         
         #other pacific island NHL
         B_pat_hypertension_18_85_NHL_otherpacificislander = T7_L2b2_C2a,
         B_num_charts_samp_hypertension_NHL_otherpacificislander = T7_L2b2_C2b,         
         B_pat_hypertension_controlled_NHL_otherpacificislander = T7_L2b2_C2c,         
         
         #black / african american NHL
         B_pat_hypertension_18_85_NHL_blackAA = T7_L2c_C2a,
         B_num_charts_samp_hypertension_NHL_blackAA = T7_L2c_C2b,         
         B_pat_hypertension_controlled_NHL_blackAA = T7_L2c_C2c,         
         
         #american indian / alaskan native NHL
         B_pat_hypertension_18_85_NHL_indianAN = T7_L2d_C2a,
         B_num_charts_samp_hypertension_NHL_indianAN = T7_L2d_C2b,         
         B_pat_hypertension_controlled_NHL_indianAN = T7_L2d_C2c,         
         
         #white NHL
         B_pat_hypertension_18_85_NHL_white = T7_L2e_C2a,
         B_num_charts_samp_hypertension_NHL_white = T7_L2e_C2b,         
         B_pat_hypertension_controlled_NHL_white = T7_L2e_C2c,         
         
         #more than one race NHL
         B_pat_hypertension_18_85_NHL_morethanone = T7_L2f_C2a,
         B_num_charts_samp_hypertension_NHL_morethanone = T7_L2f_C2b,          
         B_pat_hypertension_controlled_NHL_morethanone = T7_L2f_C2c,         
         
         #unreported NHL
         B_pat_hypertension_18_85_NHL_unreported = T7_L2g_C2a,
         B_num_charts_samp_hypertension_NHL_unreported = T7_L2g_C2b,        
         B_pat_hypertension_controlled_NHL_unreported = T7_L2g_C2c,         
         
         
         #refused race and ethnicity
         B_pat_hypertension_18_85_refused_race_eth = T7_Lh_C2a,
         B_num_charts_samp_hypertension_refused_race_eth = T7_Lh_C2b,   
         B_hypertension_controlled_refused_race_eth = T7_Lh_C2c,

         ######section C - Diabetes
         C_total_pat_diabetes_18_75 = T7_Li_C3a,
         C_total_num_charts_samp_diabetes = T7_Li_C3b,
         C_total_pat_HbAlc_under8 = T7_Li_C3d1,
         C_total_pat_HbAlc_8_9 = T7_Li_C3e,
         C_total_pat_HbAlc_over9_ornotest = T7_Li_C3f,
         #hispanic/latino + non h/l subtotals
         C_subtotal_pat_diabetes_18_75_HL = T7_LSTHL_C3a,
         C_subtotal_num_charts_samp_HL = T7_LSTHL_C3b,
         C_subtotal_pat_HbAlc_under8_HL = T7_LSTHL_C3d1,
         C_subtotal_pat_HbAlc_HbAlc_8_9_HL = T7_LSTHL_C3e,
         C_subtotal_pat_HbAlc_HbAlc_over9_ornotest_HL = T7_LSTHL_C3f,
         C_subtotal_pat_diabetes_18_75_NHL = T7_LSTNHL_C3a,
         C_subtotal_num_charts_samp_NHL = T7_LSTNHL_C3b,
         C_subtotal_pat_HbAlc_under8_NHL = T7_LSTNHL_C3d1,
         C_subtotal_pat_HbAlc_HbAlc_8_9_NHL = T7_LSTNHL_C3e,
         C_subtotal_pat_HbAlc_HbAlc_over9_ornotest_NHL = T7_LSTNHL_C3f, 
         
         #asian HL
         C_pat_diabetes_18_75_HL_asian = T7_L1a_C3a,
         C_num_charts_samp_diabetes_HL_asian = T7_L1a_C3b,         
         C_pat_HbAlc_under8_HL_asian = T7_L1a_C3d1,         
         C_pat_HbAlc_8_9_HL_asian = T7_L1a_C3e,
         C_pat_HbAlc_over9_ornotest_HL_asian = T7_L1a_C3f,         
         
         #native hawaiian HL
         C_pat_diabetes_18_75_HL_nativehawaiian = T7_L1b1_C3a,
         C_num_charts_samp_diabetes_HL_nativehawaiian = T7_L1b1_C3b,         
         C_pat_HbAlc_under8_HL_nativehawaiian = T7_L1b1_C3d1,         
         C_pat_HbAlc_8_9_HL_nativehawaiian = T7_L1b1_C3e,
         C_pat_HbAlc_over9_ornotest_HL_nativehawaiian = T7_L1b1_C3f,         
         
         #other pacific islander HL
         C_pat_diabetes_18_75_HL_otherpacificislander = T7_L1b2_C3a,
         C_num_charts_samp_diabetes_HL_otherpacificislander = T7_L1b2_C3b,         
         C_pat_HbAlc_under8_HL_otherpacificislander = T7_L1b2_C3d1,         
         C_pat_HbAlc_8_9_HL_otherpacificislander = T7_L1b2_C3e,  
         C_pat_HbAlc_over9_ornotest_HL_otherpacificislander = T7_L1b2_C3f,         
         
         #Black/african american HL
         C_pat_diabetes_18_75_HL_blackAA = T7_L1c_C3a,
         C_num_charts_samp_diabetes_HL_blackAA = T7_L1c_C3b,         
         C_pat_HbAlc_under8_HL_blackAA = T7_L1c_C3d1,         
         C_pat_HbAlc_8_9_HL_blackAA = T7_L1c_C3e,         
         C_pat_HbAlc_over9_ornotest_HL_blackAA = T7_L1c_C3f,         
         
         #american indian/alaskan native HL
         C_pat_diabetes_18_75_HL_indianAN = T7_L1d_C3a,
         C_num_charts_samp_diabetes_HL_indianAN = T7_L1d_C3b,         
         C_pat_HbAlc_under8_HL_indianAN = T7_L1d_C3d1,         
         C_pat_HbAlc_8_9_HL_indianAN = T7_L1d_C3e,         
         C_pat_HbAlc_over9_ornotest_HL_indianAN = T7_L1d_C3f,         
         
         #white HL
         C_pat_diabetes_18_75_HL_white = T7_L1e_C3a,
         C_num_charts_samp_diabetes_HL_white = T7_L1e_C2b,         
         C_pat_HbAlc_under8_HL_white = T7_L1e_C3d1,
         C_pat_HbAlc_8_9_HL_white = T7_L1e_C3e,         
         C_pat_HbAlc_over9_ornotest_HL_white = T7_L1e_C3f,         
         
         #more than one race HL
         C_pat_diabetes_18_75_HL_morethanone = T7_L1f_C3a,
         C_num_charts_samp_diabetes_HL_morethanone = T7_L1f_C3b,         
         C_pat_HbAlc_under8_HL_morethanone = T7_L1f_C3d1, 
         C_pat_HbAlc_8_9_HL_morethanone = T7_L1f_C3e,         
         C_pat_HbAlc_over9_ornotest_HL_morethanone = T7_L1f_C3f,         
         
         #unreported HL
         C_pat_diabetes_18_75_HL_unreported = T7_L1g_C3a,
         C_num_charts_samp_diabetes_HL_unreported = T7_L1g_C3b,         
         C_pat_HbAlc_under8_HL_unreported = T7_L1g_C3d1,
         C_pat_HbAlc_8_9_HL_unreported = T7_L1g_C3e,         
         C_pat_HbAlc_over9_ornotest_HL_unreported = T7_L1g_C3f,         
         
         #asian NHL
         C_pat_diabetes_18_75_NHL_asian = T7_L2a_C3a,
         C_num_charts_samp_diabetes_NHL_asian = T7_L2a_C3b,         
         C_pat_HbAlc_under8_NHL_asian = T7_L2a_C3d1,       
         C_pat_HbAlc_8_9_NHL_asian = T7_L2a_C3e,         
         C_pat_HbAlc_over9_ornotest_NHL_asian = T7_L2a_C3f,         
         
         #native hawaiian NHL
         C_pat_diabetes_18_75_NHL_nativehawaiian = T7_L2b1_C3a,
         C_num_charts_samp_diabetes_NHL_nativehawaiian = T7_L2b1_C3b,         
         C_pat_HbAlc_under8_NHL_nativehawaiian = T7_L2b1_C3d1, 
         C_pat_HbAlc_8_9_NHL_nativehawaiian = T7_L2b1_C3e,         
         C_pat_HbAlc_over9_ornotest_NHL_nativehawaiian = T7_L2b1_C3f,         
         
         #other pacific island NHL
         C_pat_diabetes_18_75_NHL_otherpacificislander = T7_L2b2_C3a,
         C_num_charts_samp_diabetes_NHL_otherpacificislander = T7_L2b2_C3b,         
         C_pat_HbAlc_under8_NHL_otherpacificislander = T7_L2b2_C3d1,         
         C_pat_HbAlc_8_9_NHL_otherpacificislander = T7_L2b2_C3e,         
         C_pat_HbAlc_over9_ornotest_NHL_otherpacificislander = T7_L2b2_C3f,         
         
         #black / african american NHL
         C_pat_diabetes_18_75_NHL_blackAA = T7_L2c_C3a,
         C_num_charts_samp_diabetes_NHL_blackAA = T7_L2c_C3b,
         C_pat_HbAlc_under8_NHL_blackAA = T7_L2c_C3d1,    
         C_pat_HbAlc_8_9_NHL_blackAA = T7_L2c_C3e,         
         C_pat_HbAlc_over9_ornotest_NHL_blackAA = T7_L2c_C3f,         
         
         #american indian / alaskan native NHL
         C_pat_diabetes_18_75_NHL_indianAN = T7_L2d_C3a,
         C_num_charts_samp_diabetes_NHL_indianAN = T7_L2d_C3b,         
         C_pat_HbAlc_under8_NHL_indianAN = T7_L2d_C3d1,      
         C_pat_HbAlc_8_9_NHL_indianAN = T7_L2d_C3e,         
         C_pat_HbAlc_over9_ornotest_NHL_indianAN = T7_L2d_C3f,         
         
         #white NHL
         C_pat_diabetes_18_75_NHL_white = T7_L2e_C3a,
         C_num_charts_samp_diabetes_NHL_white = T7_L2e_C3b,            
         C_pat_HbAlc_under8_NHL_white = T7_L2e_C3d1,    
         C_pat_HbAlc_8_9_NHL_white = T7_L2e_C3e,         
         C_pat_HbAlc_over9_ornotest_NHL_white = T7_L2e_C3f,         
         
         #more than one race NHL
         C_pat_diabetes_18_75_NHL_morethanone = T7_L2f_C3a,
         C_num_charts_samp_diabetes_NHL_morethanone = T7_L2f_C3b,         
         C_pat_HbAlc_under8_NHL_morethanone = T7_L2f_C3d1,  
         C_pat_HbAlc_8_9_NHL_morethanone = T7_L2f_C3e,         
         C_pat_HbAlc_over9_ornotest_NHL_morethanone = T7_L2f_C3f,         
         
         #unreporte NHL
         C_pat_diabetes_18_75_NHL_unreported = T7_L2g_C3a,
         C_num_charts_samp_diabetes_NHL_unreported = T7_L2g_C3b,         
         C_pat_HbAlc_under8_NHL_unreported = T7_L2g_C3d1,
         C_pat_HbAlc_8_9_NHL_unreported = T7_L2g_C3e,         
         C_pat_HbAlc_over9_ornotest_NHL_unreported = T7_L2g_C3f,         
         
         #refused race and ethnicity
         C_pat_diabetes_18_75_refused_race_eth = T7_Lh_C3a,
         C_num_charts_samp_diabetes_refused_race_eth = T7_Lh_C3b,         
         C_pat_HbAlc_under8_refused_race_eth = T7_Lh_C3d1,
         C_pat_HbAlc_8_9_refused_race_eth = T7_Lh_C3e, 
         C_pat_HbAlc_over9_ornotest_refused_race_eth = T7_Lh_C3f
         )
```

    ## Error in eval(lhs, parent, parent): object 'uds2014to2019.t7' not found

Add column of shortened health center names:

``` r
HC_short = 
  readxl::read_excel(".\\UDS_Name_&_HC_Name.xlsx", sheet = "Sheet1") 

uds2014to2019.t7_demographics = uds2014to2019.t7_demographics %>% 
  mutate(HealthCenterName_original = HealthCenterName,
    HealthCenterName = str_to_title(HealthCenterName)) %>%
  left_join(HC_short, by = "HealthCenterName") %>% 
  arrange(HC_name, ReportingYear) %>% select(HC_name, ReportingYear, everything())
```

    ## Error in eval(lhs, parent, parent): object 'uds2014to2019.t7_demographics' not found

``` r
janitor::remove_empty(uds2014to2019.t7_demographics, which = c("rows", "cols"), quiet = TRUE)
```

    ## Error in is.data.frame(x): object 'uds2014to2019.t7_demographics' not found

``` r
is.na(uds2014to2019.t7_demographics) = uds2014to2019.t7_demographics == "NaN"
```

    ## Error in eval(expr, envir, enclos): object 'uds2014to2019.t7_demographics' not found

Export excel sheet for table 6B 2014-2019:

``` r
# Create a blank workbook
OUT <- createWorkbook()

# Add some sheets to the workbook
addWorksheet(OUT, "Table 7 Demographics")

# Write the data to the sheets
writeData(OUT, sheet = "Table 7 Demographics", x = uds2014to2019.t7_demographics)
```

    ## Error in writeData(OUT, sheet = "Table 7 Demographics", x = uds2014to2019.t7_demographics): object 'uds2014to2019.t7_demographics' not found

``` r
# Reorder worksheets
#worksheetOrder(OUT) <- c(3,2,1) # no need to reorder at the moment

# Export the file
#saveWorkbook(OUT, "relevant_vars_2014to2019_T7_demographics.xlsx", overwrite = TRUE)
```
